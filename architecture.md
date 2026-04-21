# music4all.ru – Architecture Plan

## Data Model (localStorage keys)

### `m4a_users` – Array of user objects
```json
[
  {
    "id": "uuid",
    "role": "admin" | "student",
    "phone": "+79991234567",
    "passwordHash": "base64(phone+password+salt)",
    "name": "Имя Фамилия",
    "createdAt": "ISO date"
  }
]
```

### `m4a_lessons` – Array of lesson objects
```json
[
  {
    "id": "uuid",
    "title": "Название урока",
    "description": "Описание",
    "videoUrl": "https://youtube.com/...",
    "pdfUrl": "https://...",
    "createdAt": "ISO date"
  }
]
```

### `m4a_songs` – Array of song objects
```json
[
  {
    "id": "uuid",
    "title": "Название песни",
    "artist": "Исполнитель",
    "difficulty": "beginner" | "intermediate" | "advanced",
    "youtubeUrl": "https://youtube.com/...",
    "tabsChords": "текст аккордов/табулатур",
    "createdAt": "ISO date"
  }
]
```

### `m4a_assignments` – Array of assignment objects
```json
[
  {
    "id": "uuid",
    "studentId": "user_id",
    "type": "lesson" | "song",
    "contentId": "lesson_id or song_id",
    "assignedAt": "ISO date"
  }
]
```

### `m4a_progress` – Array of progress objects
```json
[
  {
    "id": "uuid",
    "studentId": "user_id",
    "type": "lesson" | "song",
    "contentId": "lesson_id or song_id",
    "completed": true | false,
    "updatedAt": "ISO date"
  }
]
```

### `m4a_session` – Current session object
```json
{
  "userId": "uuid",
  "role": "admin" | "student",
  "name": "Имя"
}
```

### `m4a_theme` – "dark" | "light"

## Views / Sections
1. `#login` – Main login page (phone + password)
2. `#admin-login` – Admin login page
3. `#admin` – Admin panel (tabs: Students, Lessons, Songs, Assignments)
4. `#dashboard` – Student dashboard (tabs: My Lessons, My Songs)

## Security Notes
- Password hash: btoa(phone + ":" + password + ":m4a_salt_2024")
- Admin credentials: +79991234567 / admin123
- Session stored in sessionStorage (clears on tab close) + localStorage option

## Sample Data
### Students
1. Иван Петров – phone: +79161234567, password: student1
2. Мария Сидорова – phone: +79261234568, password: student2

### Lessons
1. "Основы игры на гитаре" – beginner intro
2. "Аккорды Am, Dm, E" – basic chords
3. "Перебор и бой" – strumming patterns

### Songs
1. "Звезда по имени Солнце" – Кино – beginner
2. "Группа крови" – Кино – intermediate
3. "Wonderwall" – Oasis – intermediate

### Assignments
- Иван: Lesson 1, Lesson 2, Song 1, Song 2
- Мария: Lesson 2, Lesson 3, Song 2, Song 3
