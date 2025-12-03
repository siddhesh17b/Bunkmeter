# CSV Timetable Format

## Quickest Way

1. **Setup → Export Template** (get a sample CSV)
2. Edit in Excel/Notepad
3. **Setup → Import** your file
4. Done

---

## Format

```csv
Day,Time,Subject
MONDAY,09:00-10:00,Math
MONDAY,10:00-11:00,Physics
MONDAY,12:00-01:00,Lunch Break
TUESDAY,02:00-04:00,Lab (Group A) / Lab (Group B)
```

| Column | Rules |
|--------|-------|
| Day | MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY (uppercase) |
| Time | Any format: `09:00-10:00`, `8-9am`, `14:00-16:00` |
| Subject | Any name. "Lunch" is ignored. |

---

## Batch-Specific Classes

For labs where different batches have different subjects:

```csv
WEDNESDAY,03:00-04:00,CN Lab (B1&B3) / DAA Lab (B2&B4)
THURSDAY,01:00-02:30,Physics Lab (Group A) / Chemistry Lab (Group B)
```

- App **auto-detects** batch names from parentheses
- Works with any naming: `(B1&B3)`, `(Group A)`, `(Section X)`
- Select your batch in Setup tab after import

---

## Common Errors

| Error | Fix |
|-------|-----|
| Invalid CSV | Need exactly 3 columns: Day, Time, Subject |
| Invalid day | Must be uppercase: MONDAY not Monday |
| Missing days | Include all 6 days (empty subjects OK) |
| Subject not tracked | Check it doesn't contain "Lunch" |

---

## Examples

**Early classes:**
```csv
MONDAY,08:00-09:00,Extra Class
MONDAY,09:00-10:00,Math
```

**Long lab sessions:**
```csv
TUESDAY,02:00-05:00,Programming Lab
```

**Course codes:**
```csv
MONDAY,09:00-10:00,CS101 - Data Structures
```

---

**Need help?** [GitHub Issues](https://github.com/siddhesh17b/MyAttendance/issues)
