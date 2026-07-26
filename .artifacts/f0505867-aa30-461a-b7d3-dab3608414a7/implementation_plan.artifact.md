# Implementation Plan - Fixing Trash Feature

Implement the "Delete Forever" and "Restore" logic for notes in the Trash view, and ensure the UI matches the high-fidelity designs.

## User Review Required

> [!IMPORTANT]
> - **API Endpoints**: I will assume the note deletion endpoint follows the folder pattern: `POST /api/note/delete-restore`. If your backend uses a different endpoint (like a direct DELETE request), please let me know.
> - **Confirmation**: I will add a confirmation dialog for "Delete Forever" to prevent accidental data loss.

## Proposed Changes

### 1. Data Layer Completion
#### [MODIFY] [note_repository.dart](file:///Users/yornnona/Documents/flutter_app/app-note/otokhi001/lib/data/repositories/note_repository.dart)
- Add `deleteRestoreNote(int id, bool isDelete)` method.
- Add `clearTrash()` method if the API supports it.

### 2. Logic Completion
#### [MODIFY] [note_list_controller.dart](file:///Users/yornnona/Documents/flutter_app/app-note/otokhi001/lib/modules/note/note_list_controller.dart)
- Implement `deleteNoteForever(int id)` using the new repository method.
- Implement `restoreNote(int id)` using the new repository method.
- Implement `clearAllTrash()` logic.

### 3. UI Refinement
#### [MODIFY] [trash_view.dart](file:///Users/yornnona/Documents/flutter_app/app-note/otokhi001/lib/modules/trash/trash_view.dart)
- Add "Restore" and "Delete" buttons to the trash cards as shown in the screenshots.
- Connect the "Clear Trash" action in the AppBar.
- Integrate `UIHelpers.showConfirmDialog` for destructive actions.

## Verification Plan

### Manual Verification
- **Trash Flow**: Delete a note -> Go to Trash -> Verify it appears.
- **Restore**: Tap "Restore" -> Verify it returns to the main list.
- **Delete Forever**: Tap "Delete" -> Confirm -> Verify it's gone from the database.
- **Empty State**: Verify the Trash view handles empty lists gracefully.
