## ✅ **1. Get Users by Age Range**
```python
@app.get("/users/age_range")
def get_users_by_age_range(min_age: int, max_age: int, db: Session = Depends(get_db)):
    return db.query(User).filter(User.age.between(min_age, max_age)).all()
```
🔹 Finds users **between a specific age range**.

---

## ✅ **2. Get Users Excluding a Certain City (NOT Condition)**
```python
@app.get("/users/not_in_city")
def get_users_not_in_city(city: str, db: Session = Depends(get_db)):
    return db.query(User).filter(User.city != city).all()
```
🔹 Finds users **who are NOT from a specific city**.

---

## ✅ **3. Get Users Whose Name Starts with a Certain Letter**
```python
@app.get("/users/name_starts_with/{letter}")
def get_users_by_starting_letter(letter: str, db: Session = Depends(get_db)):
    return db.query(User).filter(User.name.startswith(letter)).all()
```
🔹 Finds users **whose name starts with the given letter**.

---

## ✅ **4. Get Users Who Have a Phone Number (NOT NULL)**
```python
@app.get("/users/has_phone")
def get_users_with_phone(db: Session = Depends(get_db)):
    return db.query(User).filter(User.phone.isnot(None)).all()
```
🔹 Finds users **who have a phone number** (i.e., the `phone` field is not `NULL`).

---

## ✅ **5. Get Users with Multiple Conditions (AND)**
```python
@app.get("/users/filter")
def filter_users(age: int, city: str, db: Session = Depends(get_db)):
    return db.query(User).filter(User.age >= age, User.city == city).all()
```
🔹 Finds users **above a certain age** AND **from a specific city**.

---

## ✅ **6. Get Users with Either Condition (OR)**
```python
from sqlalchemy import or_

@app.get("/users/or_filter")
def filter_users(age: int, city: str, db: Session = Depends(get_db)):
    return db.query(User).filter(or_(User.age >= age, User.city == city)).all()
```
🔹 Finds users who are **either above a certain age OR from a specific city**.

---

## ✅ **7. Get Users Ordered by Age (Sorting)**
```python
@app.get("/users/sorted")
def get_sorted_users(db: Session = Depends(get_db)):
    return db.query(User).order_by(User.age.desc()).all()  # Sort by age (descending)
```
🔹 **`asc()`** for ascending, **`desc()`** for descending.

---

## ✅ **8. Get a Limited Number of Users (Pagination)**
```python
@app.get("/users/limit")
def get_limited_users(limit: int = 10, db: Session = Depends(get_db)):
    return db.query(User).limit(limit).all()
```
🔹 Returns **only a certain number of users**.

---

## ✅ **9. Count the Number of Users**
```python
@app.get("/users/count")
def count_users(db: Session = Depends(get_db)):
    return {"user_count": db.query(User).count()}
```
🔹 **Counts the total number of users** in the database.

---
