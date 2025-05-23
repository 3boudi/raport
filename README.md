# v1.0.0  
Repository: https://github.com/3boudi/Cashier

- Simplistic business logic without algorithmic correctness safeguards (e.g., no shortest-path optimizations like Dijkstra for inventory routing).  
- Missing robust authentication & authorization middleware, exposing all endpoints to unauthorized access.  
- No network abstraction layer (e.g., missing REST client/service layer), causing tight coupling and potential race conditions under concurrent requests.  
- Legacy tech stack (jQuery, Bootstrap 4) in a monolithic architecture, impeding modularization and modern framework integration.  
- Non-responsive UI lacking adaptive layouts and ARIA accessibility compliance.  
- Zero automated tests (unit/integration), no dependency injection, high regression risk on refactoring.  
