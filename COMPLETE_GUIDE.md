# Custom Timetable Upload - Complete Guide & Implementation

## 📖 Table of Contents
1. [User Guide - CSV Format & Upload](#user-guide)
2. [Implementation Summary](#implementation-summary)
3. [Technical Details](#technical-details)
4. [Support & Troubleshooting](#support)

---

# User Guide

## Overview
MyAttendance now supports custom timetable upload! Users can create their own timetable CSV file and import it into the application with **full flexibility** for time slots, subject names, and batch names.

## CSV Format

### Structure
Your CSV file should follow this structure:
- **Column 1**: Day of the week (MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY)
- **Column 2**: Time slot (format: HH:MM-HH:MM, e.g., 09:00-10:00)
- **Column 3**: Subject details

### Example CSV:
```csv
Day,Time,Subject
MONDAY,09:00-10:00,Minor
MONDAY,10:00-11:00,DM
MONDAY,11:00-12:00,DAA
MONDAY,12:00-01:00,Lunch Break
MONDAY,01:00-02:00,TOC
MONDAY,02:00-03:00,CN
TUESDAY,09:00-10:00,Minor
TUESDAY,10:00-11:00,CN
...
```

### Important Rules:

1. **Time Slots**: ✅ **FULLY FLEXIBLE** - Use ANY time format you want!
   - Common: 09:00-10:00, 10:00-11:00, etc.
   - **Early classes**: 08:00-09:00, 07:00-08:00, 07:30-08:30
   - **Custom times**: 09:30-10:30, 14:15-15:15, 13:45-15:15
   - **Any duration**: 08:00-10:00, 13:00-16:00, 02:00-03:30
   - **No validation** - App accepts ANY time format
   - **No limit** on number of slots per day

2. **Subject Names**: ✅ **FULLY FLEXIBLE** - Use ANY subject name!
   - **No code extraction** - Names are kept exactly as entered
   - Simple: `Math`, `Physics`, `Chemistry`
   - With codes: `CS101 - Data Structures`, `MATH201`
   - With details: `Advanced Java Programming (Lab 3)`
   - **Custom names**: Anything you want!
   - Only `Lunch` keyword is excluded from attendance tracking

3. **Batch Names**: ✅ **CUSTOM BATCHES** - Not limited to B1/B3 or B2/B4!
   - Format: `Subject1 (BatchA) / Subject2 (BatchB)`
   - Default: `(B1&B3) / (B2&B4)`
   - Custom: `(GroupA) / (GroupB)`, `(Section1) / (Section2)`
   - **Any batch names** in parentheses work!

4. **Special Entries**:
   - `Lunch Break` or anything with "Lunch" - Ignored for attendance
   - Empty slots: Leave subject blank or use empty string
   - **All other names are tracked** - No restrictions!

5. **Batch-Aware Classes**:
   - Format: `Subject1 (BatchA) / Subject2 (BatchB)`
   - Example: `CN Lab (B1&B3) / DAA Lab (B2&B4)`
   - Works with custom batch names too!
   - App shows only the class for selected batch

## How to Upload

1. **Prepare Your CSV**:
   - Create a CSV file with structure above
   - Save as `my_timetable.csv` or any name you prefer
   - Ensure all days (MONDAY-SATURDAY) are included

2. **Export Template** (Optional):
   - Open MyAttendance app
   - Go to **Setup Tab**
   - Click **"📤 Export Timetable Template"** button
   - Gets current timetable exported in chronological 24-hour order
   - This generates a CSV you can modify

3. **Import Your Timetable**:
   - Go to **Setup Tab**
   - Click **"📥 Import Custom Timetable"** button
   - Select your CSV file
   - App validates days and CSV structure only
   - **No restart required** - All tabs refresh automatically
   - Success message confirms import

4. **Verify**:
   - Go to **Timetable Tab** to view imported schedule
   - Check **Mark Attendance Tab** to ensure subjects are listed correctly
   - Go to **Summary Tab** to see all tracked subjects

## Best Practices

1. ✅ **Backup First**: Export current timetable before importing new one
2. ✅ **Test Import**: Import and verify before deleting backup
3. ✅ **Consistent Naming**: Use same subject names throughout (e.g., "DAA" not "daa" or "Data Structures")
4. ✅ **Include All Days**: Always include Saturday even if no classes
5. ✅ **Clear Formatting**: Remove special characters that might cause parsing issues
6. ✅ **Upload Once**: Upload ONE complete timetable with BOTH batch schedules
7. ✅ **Batch Selection**: Select your batch in Setup tab - app automatically filters classes

## Advanced: Batch-Specific Schedule

If different batches have different labs:
```csv
Day,Time,Subject
WEDNESDAY,03:00-04:00,CN Lab (B1&B3) / DAA Lab (B2&B4)
WEDNESDAY,04:00-05:00,CN Lab (B1&B3) / DAA Lab (B2&B4)
```

This will show:
- **B1/B3 students**: CN Lab on Wednesday 3-5pm
- **B2/B4 students**: DAA Lab on Wednesday 3-5pm

## Sample CSV Files

### Minimal Example (One Day):
```csv
Day,Time,Subject
MONDAY,09:00-10:00,Math
MONDAY,10:00-11:00,Physics
MONDAY,11:00-12:00,Chemistry
MONDAY,12:00-01:00,Lunch Break
MONDAY,01:00-02:00,Biology
MONDAY,02:00-03:00,English
```

### Full Week Example:
Available in the exported template from the app.

---

# Implementation Summary

## ✅ What's Been Added

### 1. **New Files Created**
- `COMPLETE_GUIDE.md` - Comprehensive guide combining user instructions and implementation details
- `timetable_template.csv` - Sample CSV template with default timetable structure

### 2. **Updated Files**

#### `data_manager.py`
- Added `CUSTOM_TIMETABLE_FILE` constant for custom timetable storage
- **New Functions**:
  - `get_active_timetable()` - Returns custom timetable if exists, otherwise default
  - `export_timetable_to_csv()` - Export current timetable to CSV file
  - `import_timetable_from_csv()` - Import CSV and validate format
  - `reset_to_default_timetable()` - Delete custom timetable and restore default
- Updated `parse_timetable_csv()` to use active timetable
- Updated `get_subjects_for_day()` to use active timetable

#### `setup_tab.py`
- Added **Timetable Management Section** in right column with 3 buttons:
  - 📥 Import Custom Timetable
  - 📤 Export Timetable Template  
  - 🔄 Reset to Default
- **New Methods**:
  - `import_timetable()` - Handles import, reinitializes subjects, **refreshes all tabs automatically** (no restart)
  - `export_timetable()` - Exports in chronological 24-hour order
  - `reset_timetable()` - Resets to default, reinitializes subjects, refreshes all tabs
- **Added Holiday/Skipped Days Dialogs**:
  - Centered, scrollable dialogs with calendar widgets
  - Holiday dialog: 500x650, mouse wheel scrolling
  - Skipped period dialog: 500x700, mouse wheel scrolling
- Imports: `export_timetable_to_csv`, `import_timetable_from_csv`, `reset_to_default_timetable`

#### `timetable_tab.py`
- Changed import from `TIMETABLE_DATA` to `get_active_timetable`
- Updated `get_subject_for_slot()` to use active timetable

#### `.gitignore`
- Added `custom_timetable.json` to ignore custom user timetables
- Updated to exclude data.json properly

## 📋 How It Works

### User Workflow:

1. **Export Template** (Optional):
   - User clicks "📤 Export Timetable Template" in Setup tab
   - Gets current timetable as CSV file
   - Can modify this CSV with their schedule

2. **Prepare CSV**:
   - Create CSV with columns: Day, Time, Subject
   - Follow format in `COMPLETE_GUIDE.md`
   - Include all 6 days (MONDAY-SATURDAY)
   - Use 8 hourly time slots (09:00-05:00)

3. **Import Custom Timetable**:
   - Click "📥 Import Custom Timetable" in Setup tab
   - Select CSV file
   - App validates:
     - ✅ Correct columns (Day, Time, Subject)
     - ✅ Valid days (MONDAY-SATURDAY)
     - ✅ CSV structure (no time slot validation - full flexibility)
     - ✅ Shows success message
   - Timetable saved to `custom_timetable.json`
   - Subjects automatically reinitialized
   - **All tabs refresh automatically** - No restart required!

4. **Reset to Default**:
   - Click "🔄 Reset to Default"
   - Deletes `custom_timetable.json`
   - Reverts to hardcoded default timetable
   - All tabs refresh automatically - No restart required

### Technical Flow:

```
User Action → UI Button Click
    ↓
setup_tab.py method called
    ↓
data_manager.py function executed
    ↓
CSV validated/processed
    ↓
custom_timetable.json saved/deleted
    ↓
Subjects reinitialized with parse_timetable_csv()
    ↓
All tabs refreshed
    ↓
User sees updated timetable
```

### Data Structure:

**custom_timetable.json**:
```json
{
  "MONDAY": {
    "09:00-10:00": "Math",
    "10:00-11:00": "Physics",
    ...
  },
  "TUESDAY": { ... },
  ...
}
```

Same structure as hardcoded `TIMETABLE_DATA` dictionary.

## 🎯 Key Features

### ✅ Validation
- Checks CSV format (3 columns)
- Validates days (MONDAY-SATURDAY)
- Validates time slots (8 slots from 09:00-17:00)
- Shows preview before import
- Confirmation dialogs

### ✅ Backward Compatible
- Default timetable still works if no custom timetable
- `get_active_timetable()` handles fallback automatically
- No code changes needed in other modules (attendance_calendar, summary_tab)

### ✅ User-Friendly
- Clear instructions in guide
- Export template feature
- Preview and confirmation dialogs
- Success/error messages
- Reset to default option

### ✅ Batch-Aware
- Supports B1/B3 and B2/B4 batch labs
- Format: `Subject (Location) (B1&B3) / Subject (Location) (B2&B4)`
- Automatically filters based on selected batch

## 📝 CSV Format Rules

### Required Structure:
```csv
Day,Time,Subject
MONDAY,09:00-10:00,Math
MONDAY,10:00-11:00,Physics
...
```

### Time Slots (8 required per day):
- 09:00-10:00
- 10:00-11:00
- 11:00-12:00
- 12:00-01:00
- 01:00-02:00
- 02:00-03:00
- 03:00-04:00
- 04:00-05:00

### Subject Formats:
- Simple: `Math`, `Physics`, `Chemistry`
- Clean names: `DM`, `DAA`, `TOC`, `CN` (default timetable uses clean names - NO course codes)
- Labs: `CN Lab`, `DAA Lab`, `Software Lab`
- Batch-specific: `CN Lab (B1&B3) / DAA Lab (B2&B4)`
- Custom: `Advanced Programming`, `CS101 - Data Structures`, anything you want!
- Special: `Lunch Break` (excluded from tracking)

### Subject Name Handling:
✅ **FULL FLEXIBILITY** - The app keeps all subject names as-is (NO EXTRACTION):
- `Data Structures and Algorithms` → `Data Structures and Algorithms` (kept as-is)
- `Math 101` → `Math 101` (kept as-is)
- `DM`, `DAA`, `TOC` → Kept as-is
- Only excludes names containing "Lunch"
- **No parsing, no extraction, no modifications**

## 🔧 Error Handling

### Import Errors:
- **Invalid CSV format**: Shows error, asks for correct format
- **Missing columns**: Shows error with required columns
- **Invalid day**: Shows warning, skips that row
- **Invalid time**: Shows warning, skips that row
- **Missing days**: Asks user to confirm or cancel

### Export Errors:
- **File write error**: Shows error message
- **No permission**: Shows error message

### Runtime:
- **Custom file corrupt**: Falls back to default timetable
- **Custom file missing**: Uses default timetable

## 📚 Documentation

### For Users:
- This file - Complete guide and implementation details
- `timetable_template.csv` - Working example
- In-app instructions in Setup tab
- Export feature to see proper CSV format

### For Developers:
- All functions have docstrings
- Code comments explain logic
- Follows existing code style
- Author credits in all 7 Python files

## 🎯 Recent Updates

### Performance & UX Improvements:
- ✅ **Centered Windows**: Main window and all dialogs centered on screen
- ✅ **No Restart Required**: Import/export refresh all tabs automatically
- ✅ **Smooth Performance**: Deferred refresh logic, optimized widget destruction
- ✅ **Mouse Wheel Scrolling**: Enabled on all tabs, treeviews, and dialogs
- ✅ **Chronological Export**: CSV exports in 24-hour sorted order
- ✅ **Right-Click Hint**: UI hint in calendar explaining right-click functionality
- ✅ **Distinct Colors**: Dark red (#EF5350) for completely skipped days vs light red for partial absences
- ✅ **Scrollable Dialogs**: Holiday and skipped period dialogs with calendar widgets and scrolling

## 🚀 Testing Checklist

✅ Export template works
✅ Import valid CSV works
✅ Import invalid CSV shows errors
✅ Reset to default works
✅ Timetable tab shows custom timetable
✅ Attendance marking works with custom subjects
✅ Summary tab shows custom subjects
✅ Batch-aware labs work with custom timetable
✅ Fallback to default if custom file missing
✅ Subject reinitialization preserves existing data

## 💡 Future Enhancements

Possible improvements:
- 📝 In-app CSV editor (no need for external file)
- 🌐 Import from Google Calendar
- 📱 QR code sharing (share timetable via QR)
- ☁️ Cloud storage integration
- 🔄 Timetable versioning (multiple semesters)
- 📊 Timetable comparison tool
- 🎨 Visual timetable builder (drag-and-drop)

---

# Support

## Troubleshooting

### CSV Format Errors
- **Error**: "Invalid CSV format"
  - **Fix**: Ensure CSV has 3 columns: Day, Time, Subject
  - Check for missing commas or extra columns

### Time Slot Issues
- ✅ **No validation** - App accepts ANY time format
- Use format HH:MM-HH:MM for consistency
- Examples: `09:00-10:00`, `08:00-09:00`, `14:15-15:15`

### Missing Days
- **Error**: "Missing required days"
  - **Fix**: Include all days from MONDAY to SATURDAY
  - Each day can have any number of time slots

### Subjects Not Appearing
- **Issue**: Subject not showing in attendance
  - **Check**: Subject name doesn't contain "Lunch"
  - All other subjects are tracked automatically

### Dialog Window Errors
- **Error**: "invalid command name" in terminal
  - **Fixed**: Dialogs now use local bind instead of bind_all
  - Mouse wheel scrolling works without errors

## 📞 Support Channels

For issues or questions:
1. Check this guide first
2. Review the exported template for correct format
3. Ensure CSV encoding is UTF-8
4. Try export then re-import to test
5. Reset to default if issues persist
6. Contact: [GitHub Issues](https://github.com/siddhesh17b/MyAttendance/issues)

---

**Author**: Siddhesh Bisen  
**GitHub**: https://github.com/siddhesh17b  
**Project**: MyAttendance - Smart Attendance Tracker  
**Version**: 1.0 with Custom Timetable Upload + Performance Optimizations
