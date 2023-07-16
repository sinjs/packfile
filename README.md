# The Packfile specification

Current version: `v0` in phase `develop`

Last updated: 16th of July 2023, see latest commit

## Introduction

The Packfile is a file in the JSON format, which describes a Minecraft modpack and its containing mods, where download the mods, and the metadata of the mods. This file can be used to automatically update the required mods for a Server or generally a modpack, or just download them.

Manually updating a modpack is really annoying for players, that just want to play on a server, and can get really complicated really fast, e.g. due to mismatched mod loaders, mod versions and in general added / removed mods.

The Packfile format however, does not guarantee auto updating, it only provides a base for clients to implement automatic updating or fetching of mods.

## Schema

The json schema is located in the [`packfile.schema.json`](packfile.schema.json) file

### Root

The root is of type `object` and contains the following properties:

| Property | Type   | Required? | Schema Reference                   |
| -------- | ------ | --------- | ---------------------------------- |
| meta     | object | yes       | [#/$defs/metadata](#defs-metadata) |
| mods     | array  | yes       | items: [#/$defs/mod](#defs-mod)    |
| loader   | number | yes       | none                               |

#### Notes

Property **loader** is an enum, with the following values:

| Name   | Value |
| ------ | ----- |
| Fabric | 0     |
| Forge  | 1     |
| Quilt  | 2     |

<span id="defs-metadata"></span>

### Metadata (`$defs/metadata`)

The metadata is of type `object` and contains the following properties:

| Property    | Type   | Required? | Schema Reference    |
| ----------- | ------ | --------- | ------------------- |
| name        | string | yes       | none                |
| description | string | yes       | none                |
| author      | string | yes       | none                |
| version     | string | yes       | [#/$defs/version]() |
| website     | string | no        | none                |
| icon        | string | no        | none                |

#### Notes

Property **icon** and **website** must contain a valid URL, the **icon** must be in **png** format.

<span id="defs-mod"></span>

### Mod (`$defs/mod`)

The mod is of type `object` and contains the following properties:

| Property | Type   | Required? | Schema Reference                   |
| -------- | ------ | --------- | ---------------------------------- |
| download | string | yes       | none                               |
| meta     | object | yes       | [#/$defs/metadata](#defs-metadata) |

<span id="defs-version"></span>

### Version (`$defs/version`)

The version is of type `string` and contains a version in the [SemVer (Semantic Versioning) format](https://semver.org/)

#### Example:

```jsonc
{
  "version": "1.2.4"
}
```

## Examples of Packfiles

A list of examples are located in the [examples directory](./examples/).

## Implementations

This is a list of implementations for various languages for parsing a Packfile:

| Language                | Implementation                                         |
| ----------------------- | ------------------------------------------------------ |
| TypeScript / JavaScript | [packfile-ts](https://npmjs.com/@packfile/packfile-ts) |

### Clients

| Client              | Operating System      | Written In       |
| ------------------- | --------------------- | ---------------- |
| [PackfileManager]() | Windows, Linux, MacOS | Rust, TypeScript |

### Adding implmentations

Open an issue if you want to add an implementation to this list.
