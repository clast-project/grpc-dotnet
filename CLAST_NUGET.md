# Clast republish

This is a **Clast** package — an independent republish (from the [`clast-project`](https://github.com/clast-project) fork) of `Grpc.Auth`. **It is not an official gRPC or Google package and is not affiliated with or endorsed by either.**

**How it differs from the upstream `Grpc.Auth` package:**

- It is re-pointed to **`Clast.Google.Apis.Auth`** — the Newtonsoft-free, source-generated `System.Text.Json` republish of `Google.Apis.Auth` — instead of the published Newtonsoft-based package. This lets the gRPC credential path participate in a fully **trimming / Native-AOT compatible** dependency closure.
- A **`net10.0`** target is added (alongside `netstandard2.0` and `net8.0`).
- **Namespaces and public type names are unchanged** (`Grpc.Auth.GoogleGrpcCredentials`, etc.). Only the package id, assembly name, and strong-name key differ, so you recompile against the `Clast.*` packages rather than dropping them in as binary replacements.

It exists so `Clast.Google.Api.Gax.Grpc` (and the gRPC-based Cloud client libraries built on it, e.g. `Google.Cloud.BigQuery.Storage.V1`) can be consumed under Native AOT: the published `Grpc.Auth` hard-binds the published `Google.Apis.Auth`, which would collide with the renamed `Clast.Google.Apis.Auth`.

Full design notes and the behavior-change catalogue live in the [`clast-project/google-api-dotnet-client`](https://github.com/clast-project/google-api-dotnet-client) repository (`PLAN.md`, `BEHAVIORAL-CHANGES.md`).
