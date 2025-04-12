# API Specification - Version 0.1.0

## Base URL

```
http://localhost:8080/api/
```

---

## Endpoints

### 1. `GET /api/form`

#### Description:

Fetches the form configuration including required fields and item list.

#### Response Example:

``` json
{
  "fields": ["Borrower Name", "Date", "Purpose"],
  "items": [
    { "name": "Card Game", "count": 2 },
    { "name": "Board Game", "count": 1 }
  ]
}
```

---

### 2. POST /api/submit

#### Description:

Submit a lending form. The data is saved as a log and inventory is updated.

#### Request Body:

``` json
{
  "borrower": "John Doe",
  "date": "2025-04-12",
  "purpose": "Presentation",
  "items": [
    { "name": "Card Game", "count": 1 },
    { "name": "Board Game", "count": 1 }
  ]
}
```

#### Response Example:

``` json
{
  "status": "success",
  "message": "Lending log saved successfully"
}
```

---

### 3. GET /api/status

#### Description:

Returns the current availability status of all items.

#### Response Example:

``` json
[
  { "name": "Card Game", "available": 2 },
  { "name": "Board Game", "available": 1 }
]
```

---

## File-Based Backend Behavior
-	Lending logs are saved to: logs/YYYY-MM-DD-HHMMSS.json
- Inventory state is updated in: state/inventory.json
- Git operations:
	-	git add logs/ state/
	-	git commit -m "Update: New lending entry"
	- git push

---

## Notes

- All data is saved locally and pushed to a local GitLab server for tamper-proof logging.
- No authentication is required (assuming a trusted local environment).
- Configuration is based on editable YAML files in the config/ directory.
