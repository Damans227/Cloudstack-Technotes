# CloudStack developer stack 
               
                ┌─────────────────────────────────────────────────────────────┐
                │                  macOS (your laptop)                        │
                │   ┌───────────────────────────────────────────────────────┐ │
                │   │   SSH tunnel → Jetty (localhost:8080/client)          │ │
                │   │   Browser → Vue UI (localhost:8081)                   │ │
                │   └───────────────────────────────────────────────────────┘ │
                └─────────────────────────────────────────────────────────────┘

                                     ⬇ (SSH)

                ┌─────────────────────────────────────────────────────────────┐
                │                  Linux Dev VM (192.168.2.200)               │
                │                                                             │
                │ ┌─────────────────────────────────────────────────────────┐ │
                │ │      CloudStack Management Server (Java monolith)       │ │
                │ │                                                         │ │
                │ │  [Runs in Jetty]                                        │ │
                │ │    - API layer                                          │ │
                │ │    - Orchestration, DB access, plugins, schedulers      │ │
                │ │                                                         │ │
                │ │  [Talks to these via internal APIs / DB / NFS]          │ │
                │ └─────────────────────────────────────────────────────────┘ │
                │                                                             │
                │ ┌────────────────────────────┐  ┌─────────────────────────┐ │
                │ │      MySQL Server          │  │     NFS Server          │ │
                │ │  - CloudStack DB           │  │  - Primary/Secondary    │ │
                │ │  - Used by mgmt server     │  │    storage mounts       │ │
                │ └────────────────────────────┘  └─────────────────────────┘ │
                │                                                             │
                │ ┌─────────────────────────────────────────────────────────┐ │
                │ │        CloudStack Agent (Simulator or KVM)              │ │
                │ │  - Talks to libvirt (in KVM mode)                       │ │
                │ │  - Runs commands from management server                 │ │
                │ │  - Pretends to be a hypervisor if using simulator       │ │
                │ └─────────────────────────────────────────────────────────┘ │
                │                                                             │
                │ ┌─────────────────────────────────────────────────────────┐ │
                │ │                libvirt + KVM (Optional)                 │ │
                │ │  - Only used in real hypervisor mode (KVM/Xen/VMware)   │ │
                │ │  - Not involved in simulator mode                       │ │
                │ └─────────────────────────────────────────────────────────┘ │
                └─────────────────────────────────────────────────────────────┘
