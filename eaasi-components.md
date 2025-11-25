# Next Gen EAASI Components

The EAASI platform combines the functions of a number of underlying software components working in concert. For the purposes of [re-architecting the system for Next Gen EAASI](https://github.com/orgs/eaasi/projects/5), it was helpful to break these components into distinct, named repos (to increase modularity of development and deployment and assist with increasing accuracy of work estimates).

Because some of these names and components are now visible on the public roadmap, this glossary of Next Gen EAASI platform components is intended to assist with clarity and transparency of planned work.

Some components are fully unique to the EAASI platform; some are custom implementations of other, well-adopted open source projects. Each component should have a corresponding [EAASI Helm Chart](https://github.com/eaasi/helm-charts) and/or dedicated repository in the EAASI GitHub group.

## Back-End

### [Superhighway](https://github.com/eaasi/superhighway)

The core EAASI API server, coordinating and executing all EAASI-specific application logic and features. The Superhighway communicates with other components to complete its tasks:

- user management tasks and access token verification check the [Guestlist](#guestlist) API
- access requests check the [Authorizer](#authorizer) API
- structured application data is stored in the Postgres [database](#database)
- user/resource data is stored and moved to/from [archives](#archives) via S3 API

One of the central tasks of the Superhighway (and the EAASI application in general) is to schedule and coordinate [EmuComp](#emucomp) pods necessary for running and interacting with remote emulation sessions.

### [EmuComp](https://github.com/eaasi/emucomp)

Every emulation session requested by a user triggers the creation of an EmuComp (Emulation Component) pod that sets up and manages the emulation session. EmuComps run specified, containerized emulator applications and expose various input/output streams to the user via the [Teleport](#teleport) web client.

### [OnRamp](https://github.com/eaasi/onramp)

The OnRamp is a reverse prozy necessary to convert the [Superhighway's](#superhighway) native (gRPC-based) API to a compatible REST API for non-gRPC clients (such as [Teleport](#teleport) and the [EAASI CLI](#eaasi-cli).

### Database

A PostgreSQL-compatible database containing structured application data (resource metadata, emulator info, user account data, etc.).

### Guestlist

The Guestlist Helm Chart defines an EAASI-specific, custom combination of authentication and identity management services provided by the [Ory](https://www.ory.com/) project. User identity metadata is stored in the [database](#database).

### Authorizer

The Authorizer Helm Chart defines an EAASI-specific, custom configuration of [OpenFGA](https://openfga.dev/) for enforcement of fine-grained access policies on resource data.

### Archives

EAASI resource data is stored in a series of S3-compatible storage buckets refered to as *archives*. There are separate, configurable archives for Images (encompassing both Environment and stand-alone Computer Image resources), Software objects, and Content objects.


## Front-End

### [Speakeasy](https://github.com/eaasi/speakeasy)

The [Guestlist](#guestlist) only provides headless API services, so a simple, custom EAASI SPA (Single-Page Application) is necessary to allow self-service identity management workflows (logging in, resetting passwords).

### [Teleport](https://github.com/eaasi/teleport)

The official EAASI web application (historically referred to as the "EaaSI UI" and/or "EaaSI Client" during EAASI's grant-funded phase). Written in Vue.js.

### [EAASI CLI](https://github.com/eaasi/cli)

An official command-line client for interacting with a deployed, running EAASI installation; mostly aimed at [Deployment Administrators](https://github.com/eaasi/roadmap/blob/main/user-definitions.md) and some user and emulator management tasks. Exact details and scope TBD.
