# Authorization Test Report   

## 1. Completed List

| URL | Method | Guest | Reserver | Administrator |
|-----|--------|-------|----------|---------------|
| / | GET | Accessible | Accessible | Accessible |
| /login | GET | Accessible | Accessible | Accessible |
| /register | GET | Accessible | Accessible | Accessible |
| /profile | GET | Not Found | Accessible (own) | Accessible |
| /reservations | GET | Unauthorized | Accessible (own) | Accessible (all) |
| /admin | GET | Not Found | Not Found | Accessible |
| /admin/users | GET | Not Found | Not Found | Accessible |
| /admin/resources | GET | Not Found | Not Found | Accessible |
| /api | GET | Not Found | Not Found | Accessible |
| /api/users | GET | Exposed (all users) | Exposed (all users) | Accessible |
| /api/reservations | GET | Exposed (all reservations) | Own reservations | All reservations |
| /api/reservations/{id} | GET | Unauthorized | Own / others | All |
| /api/resources | GET | Empty | Accessible | Accessible |
| /debug | GET | Not Found | Not Found | Not Found |
| /config | GET | Not Found | Not Found | Not Found |
| /.env | GET | Not Found | Not Found | Not Found |
| POST /api/reservations | POST | 404 Not Found | Accessible (own) | Accessible |
| PUT /api/reservations/{id} | PUT | 404 Not Found | Own reservation accessible / others 404 | Accessible |
| DELETE /api/reservations/{id} | DELETE | 404 Not Found | Own reservation accessible / others 404 | Accessible |
| POST /api/resources | POST | 404 Not Found | 404 Not Found | Accessible |

## 2. Findings

### Guest

- **Can access:** `/`, `/login`, `/register`, buttons work    
- **Cannot access:** `/profile`, `/reservations`, `/admin`, `/admin/users`, `/admin/resources`, `/debug`, `/config`    
- **Critical:** `/api/users` and `/api/reservations` are exposed and return all users and reservations    
- POST, PUT, DELETE actions fail with 404 Not Found 
- Frontend disables “Add Resource” / “Add Reservation” buttons for Guest    
- Unauthorized access to sensitive data (user accounts and reservations) is a critical vulnerability    

### Reserver

- Can:  
  - Book resource  
  - View own reservations  
  - Edit own reservation  
  - Delete own reservation  
- Cannot access admin endpoints (`/admin`, `/admin/users`, `/admin/resources`) -> backend correctly blocks    
- **Issue:** `/api/users` exposed, lists all users including administrators    
- Accessing `/api/reservations/2` shows reservation belonging to administrator -> potential IDOR / data exposure    
- PUT / DELETE on reservations not owned by Reserver -> 404  
- Data exposure of other user's reservations   

### Administrator

- Can:  
  - Add / delete resources  
  - View all reservations  
  - Modify / delete reservations 
- `/debug`, `/config`, `/.env` -> Not Found  
- `/api/users` lists all users    
- All administrative actions function    
- Cannot see raw passwords  
- Administrator access is correctly enforced, no issues found    

## 3. Summary of Role Capabilities

| Role | Can View | Can Modify | Notes |
|------|-----------|------------|---------------|
| Guest | Public pages only | None | APIs exposed -> critical |
| Reserver | Own reservations, public resources | Own reservations | Cannot access admin, but can see all users -> high risk |
| Administrator | All pages & resources | Full control | Permissions correctly enforced, no exposed debug/config | 
