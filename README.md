# [ARCHIVED]

# POC of bug in angular CLI for pnpm monorepo (angular version 18 and 19 in the same repo)

This is a basic setup of monorepo with heterogenous angular versions (18 and 19).
It demonstrate an unexpected version intercation that produce a blocking issue building/testing the angular 19 project.

## Reproduction Steps

``` bash
pnpm install
cd ng-19
pnpm run build
```

eg:
```
❯ pnpm run build

> ng-19@0.0.0 build /tmp/monorepo_angular_18_19/ng-19
> ng build

This version of CLI is only compatible with Angular versions ^18.0.0,
but Angular version 19.1.3 was found instead.
Please visit the link below to find instructions on how to update Angular.
https://update.angular.dev/
 ELIFECYCLE  Command failed with exit code 3.
```

Running `pnpm run version` demonstrate that it's not a basic dependency issue :
```
❯ pnpm run -r version
Scope: 2 of 3 workspace projects
ng-18 version$ ng --version
│ 18.2.12
└─ Done in 340ms
ng-19 version$ ng --version
│ 19.1.4
└─ Done in 340ms
```

## Initial setup

angular project were created using :
``` bash
pnpx @angular/cli@19 new --package-manager pnpm ng-19 --skip-install
pnpx @angular/cli@18 new --package-manager pnpm ng-18 --skip-install
```
