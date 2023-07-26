## DevOps for Kong

This repo contains workflows to sync Kong configs to your kong instances.

```text
                        ┌───────────┐
                        │    CA     │
                        └─────┬─────┘
                            Cert                            ┌──────┐
                        ┌─────▼─────┐    ┌────────────┐  ┌──► SVC1 │
                        │           │    │            ├──┘  └──────┘
                        │           │    │ ┌────────┐ │     ┌──────┐
┌──────────┐            │           │    │ │ proxy  │ ├─────► SVC2 │
│ API      │            │           │    │ └────────┘ │     └──────┘
│ Consumer ├──Requests──►    ALB    ├────►            │     ┌──────┐
└──────────┘            │           │    │ ┌────────┐ ├─────► SVC3 │
                        │           │    │ │  Admin │ │     └──────┘
                        │           │    │ │   API  │ │     ┌──────┐
                        │           │    │ └────────┘ ├─────► SVC4 │
                        │           │    │       ┌────┤     └──────┘
                        │           │    │       │Kong├──┐  ┌──────┐
                        └─────▲─────┘    └───────┴────┘  └──► SVC5 │
                    ▲─────────┴──────────────◄──────────┐   └──────┘
┌───────────────────┼───────────────────────────────────┼──────────┐
│ ┌──────────┐ ┌────┴─────┐ ┌──────────┐ ┌──────────┐ ┌─┴────────┐ │
│ │ Kong     │ │   Sync   │ │   diff   │ │ validate │ │   Ping   │ │
│ │ Configs  │ │          ◄─┤          ◄─┤          ◄─┤          │ │
│ └─────┬────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ └────┬─────┘ │
│       │           │            │            │     ┌──────┘       │
│       │   ┌───────┴────────────┴────────────┴───┐ │              │
│       └───►                decK                 ├─┘  ┌───────────┤
│           └─────────────────────────────────────┘    │  GitHub   │
│                                                      │  Actions  │
└──────────────────────────────────────────────────────┴───────────┘
```

This workflow assume you have authentication for Admin API and you are familiar with [decK](https://github.com/Kong/deck).

For detail information, please check blog post [here](https://tech.aufomm.com/how-to-use-github-action-to-manage-kong-configs-in-ci-cd-pipelines/).