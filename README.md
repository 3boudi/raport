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
