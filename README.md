# v1.0.0  
Repository: https://github.com/3boudi/Cashier

- Simplistic business logic without algorithmic correctness safeguards (e.g., no shortest-path optimizations like Dijkstra for inventory routing).  
- Missing robust authentication & authorization middleware, exposing all endpoints to unauthorized access.  
- No network abstraction layer (e.g., missing REST client/service layer), causing tight coupling and potential race conditions under concurrent requests.  
- Legacy tech stack (jQuery, Bootstrap 4) in a monolithic architecture, impeding modularization and modern framework integration.  
- Non-responsive UI lacking adaptive layouts and ARIA accessibility compliance.  
- Zero automated tests (unit/integration), no dependency injection, high regression risk on refactoring.  
- Architectural limitations will hinder building a scalable hypermarket system. 
# v1.1.0  
Repository: https://github.com/3boudi/supermark-mengent-laravel

- Refactored routing using Laravel’s `Route::resource` and middleware groups, enforcing strict MVC separation in Controllers, Models, and Views.  
- Migrated raw SQL to Eloquent ORM with query builder and eager loading, yielding measurable performance improvements under load.  
- Leveraged Service Providers and the IoC container, enabling `php artisan route:cache` and `config:cache` for faster request lifecycle.  
- Exposed RESTful API endpoints for Hypermarket ↔ Supermarket ↔ Cashier synchronization via Laravel Passport (OAuth2), but lacks real-time broadcasting  and robust retry logic.  
- Frontend still built on basic Blade templates without responsive Flexbox/Grid or component-based JS framework, causing inconsistent UX across devices.  
- Zero automated integration or end-to-end tests (PHPUnit/Laravel Dusk) for cross-system workflows, risking regressions on future refactors.  
- Remaining UI and network-layer gaps will hinder seamless orchestration of the hypermarket–supermarket–cashier ecosystem.  
# v1.1.1  
Repository: https://github.com/3boudi/supermark-mengent-laravel

- Enhanced multi-role authentication with Laravel Sanctum guards and custom Gates/Policies for `admin`, `manager`, and `cashier`.  
- Optimized performance via Redis query caching (`Cache::remember`), queue-based order processing (Laravel Queues + Horizon), and eager-loaded relationships.  
- Refined Blade UI with responsive Flexbox/Grid layouts, Livewire components for real-time validation, and ARIA-compliant accessibility fixes.  
- Introduced a `GraphService` implementing Dijkstra’s algorithm using adjacency lists and a binary min-heap for optimal goods-routing between hypermarket nodes.  
- Refactored network sync to use Laravel Events/Broadcasting (Pusher) for near real-time Hypermarket↔Supermarket↔Cashier updates.  
- Added PHPUnit unit tests for auth workflows and feature tests for cart/order lifecycle, raising code coverage baseline.  
- These enhancements lay the groundwork for a scalable, performant hypermarket system with intelligent routing and secure role-based access.  
# v1.1.2  
Repository: https://github.com/3boudi/supermark-mengent-laravel

- Switched transport from HTTP/AJAX to raw PHP TCP/IP sockets, implementing persistent socket streams for inter-user communication.  
- Custom MessageBroker service lacks proper framing (no length-prefix or delimiter), causing packet fragmentation, reassembly bugs, and data corruption.  
- Nagle’s algorithm enabled by default introduces head-of-line blocking and latency spikes under concurrent load—missing TCP_NODELAY tuning.  
- Blocking I/O design leads to thread starvation, elevated CPU usage, and unpredictable request-response times between users.  
- No robust error-handling for socket disconnects or timeouts, resulting in stale connections and memory leaks over prolonged uptime.  
- Absence of fallback protocols (e.g., HTTP long-polling or WebSockets) causes failures behind NAT/firewalls and degrades reliability.  
- These TCP/IP networking limitations critically undermine real-time sync and will obstruct scaling the hypermarket ecosystem.  
# v1.1.3  
Repository: https://github.com/3boudi/supermark-mengent-laravel

- Reverted to HTTP/REST transport using HTTP/2 multiplexing and persistent Keep-Alive connections for inter-service calls, drastically reducing latency.  
- Consolidated API endpoints under a unified OpenAPI spec but lacking semantic versioning, causing contract drift between modules.  
- Improved throughput with Guzzle HTTP client pooling and Circuit Breaker pattern (via Symfony’s HttpClient), boosting resilience under load.  
- Exposed JSON:API–compliant resources for `admin_hypermarket`, `manager_supermarket`, and `cashier_cashier`, but inconsistent field naming and payload schemas across these interfaces.  
- Implemented Cross-Origin Resource Sharing (CORS) policies and rate-limiting middleware, yet missing centralized API Gateway or API version negotiation.  
- Frontend Blade components still vary in data-binding conventions (Vue vs. Livewire), leading to UI state desynchronization and edge-case rendering bugs.  
- Persistent schema mismatches and lack of interface contracts will impede seamless integration across hypermarket, supermarket, and cashier domains.  
# v1.2.0  
Repository: https://github.com/3boudi/supermark-mengent-laravel

- Frontend rewritten in Next.js with SSR/SSG, React Hooks for state management, and Tailwind CSS for utility-first styling.  
- Backend remains Laravel API, fully decoupled via REST endpoints consumed with `fetch` (or Axios) in Next.js.  
- All core use cases (product search, cart, checkout, sales history, role-based dashboards) re-implemented end-to-end with consistent request/response schemas.  
- Admin (Hypermarket) interface rebuilt using Filament Laravel — leveraging customizable Resources, Tables, and Forms for CRUD.  
- Unified OpenAPI spec with versioned routes (`/api/v2/...`), strong typing via JSON Schema, and automatic client generation.  
- Improved data validation: Laravel FormRequests + Zod schemas in Next.js, ensuring contract integrity on both client and server.  
- Performance optimizations: ISR (Incremental Static Regeneration), Laravel route & config caching, and optimized DB queries with indexed columns.  
# v1.2.1  
Repository: https://github.com/3boudi/supermark-mengent-laravel

- Repackaged as a desktop application using Electron.js with a multi-process architecture (main + renderer) for high-performance rendering.  
- Bundled all Node and NPM dependencies via `electron-builder`, enabling single-step packaging and cross-platform binaries.  
- Implemented IPC channels (`ipcMain`/`ipcRenderer`) for secure communication between frontend (Electron) and backend (Laravel API) over local network WebSockets.  
- Added custom `appConfig.json` loader to inject Twitter API credentials at runtime, enabling automatic tweet-posting of sales events via OAuth 2.0.  
- Enabled `AutoLaunch` on OS startup with `electron-auto-launch`, so the app boots and connects to the server without manual intervention.  
- Configured `contextIsolation` and `nodeIntegration` policies to harden security while allowing native modules .
- Integrated Electron’s `autoUpdater` (Squirrel) for seamless version rollouts, ensuring users stay on the latest build without manual downloads.  
