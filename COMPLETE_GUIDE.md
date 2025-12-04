# Complete Guide

## Custom Timetable Import

### Quick Steps
1. **Setup Tab** → **Export Timetable Template**
2. Edit the CSV file with your classes
3. **Setup Tab** → **Import Custom Timetable**
4. Pick your batch → Done

### CSV Format (3 columns, no header)
```
MONDAY,09:00-10:00,Mathematics
MONDAY,10:00-11:00,Physics  
MONDAY,11:00-12:00,Lunch
MONDAY,02:00-04:00,CN Lab (B1&B3) / DAA Lab (B2&B4)
TUESDAY,09:00-10:00,Chemistry
```

### Rules
- **Days**: MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY (uppercase)
- **Time**: Any format works (09:00-10:00, 9-10, 0900-1000)
- **Subject**: Any name. "Lunch" is auto-skipped.
- **Batches**: `Subject1 (Batch1) / Subject2 (Batch2)` - app shows correct one based on your selection

### After Import
- Old attendance data is cleared (fresh start)
- Check Timetable Tab to verify
- Batch options auto-update from your CSV

---

## How Attendance Works

### Present by Default
- All classes until TODAY are marked **present** automatically
- You only mark **absences** (less clicking)
- Future dates can't be marked

### Marking Absences
- **Left-click date** → Side panel with checkboxes per subject
- **Right-click date** → Mark entire day absent instantly
- Right-click again → Restore all to present

### Multiple Classes Same Day
If Physics Lab appears twice on Monday (2 slots), each is tracked separately.
You'll see:
- Physics Lab (Class #1) ☑
- Physics Lab (Class #2) ☑

---

## Holidays & Skipped Days

### Holidays
- Don't count toward attendance calculation
- Add in Setup Tab → Holiday Periods
- Can also left-click date → "Mark as Holiday" button

### Skipped Days (Sick Leave, etc.)
- When you miss the ENTIRE day
- Add in Setup Tab → Skipped Periods
- Or just right-click the date in calendar
- Automatically marks all subjects absent for those days

---

## Summary Dashboard Features

### Stats Cards (Top)
- 📚 Total Subjects
- 📊 Average Attendance %
- ✅ Excellent + Safe count
- ⚠️ At Risk count

### Semester Progress Bar
- Shows % of semester completed
- Color: Green (early) → Yellow (mid) → Red (ending soon)
- "X days left" badge

### Subject Table
| Column | Meaning |
|--------|--------|
| Attended | Classes you were present |
| Total | Classes held so far |
| Remaining | Future classes till semester end |
| Percentage | Your attendance % |
| Progress | Visual bar |
| Status | 🟢 Excellent (≥85%) / 🟡 Safe (75-84%) / 🔴 At Risk (<75%) |
| Can Skip | How many more classes you can bunk |

### Subject Details Panel (Click any row)
- Attended / Total / Remaining breakdown
- List of all absent dates
- **Recovery calculation**: "Need X more classes to reach 75%" (if at risk)

### Manual Override (Double-click any row)
For when auto-calculation is wrong:
- Professor cancelled class
- Extra class was held
- You attended a makeup class

Set exact total and attended → Overrides auto-calculation.

---

## The 75% Formula

```
Safe to Skip = floor((Attended - 0.75 × Total) / 0.25)
```

Example:
- Attended: 30, Total: 36
- (30 - 27) / 0.25 = 12 classes safe to skip

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Wrong attendance % | Check semester dates, verify no absences marked by mistake |
| Subject shows 0 classes | Semester hasn't started yet for that day |
| "Remaining" shows 0 | Semester ended or subject not in future schedule |
| Import failed | Check CSV format - days uppercase, no header row |
| Batch not showing | Your CSV needs batch format: `Subject (BatchName)` |
| Data looks wrong | Setup Tab → Reset Data (clears absences, keeps dates) |
| Want completely fresh start | Delete `data.json` and `custom_timetable.json`, restart app |

---

## Mouse/Keyboard Actions

| Action | How |
|--------|-----|
| Mark day absent | Right-click date |
| Mark day present | Right-click already-skipped date |
| See subject details | Single-click row in Summary |
| Override attendance | Double-click row in Summary |
| Sort table | Click column header |
| Scroll dashboard | Mouse wheel (not over table) |
| Scroll table | Mouse wheel over table |

---

## Data Files

| File | Contents | Safe to Delete? |
|------|----------|----------------|
| `data.json` | All your attendance data | NO - you'll lose everything |
| `custom_timetable.json` | Your imported timetable | Yes - reverts to default |

Backup `data.json` if you want to save your data.

---

## Reset Options

| What | How | Effect |
|------|-----|--------|
| Clear absences only | Setup → Reset Data | Keeps dates, clears attendance |
| Reset timetable | Setup → Reset to Default | Removes custom timetable |
| Full reset | Delete data.json + restart | Fresh install state |
