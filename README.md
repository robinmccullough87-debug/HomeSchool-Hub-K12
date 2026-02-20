# HomeSchool-Hub-K12
An interactive learning platform with progress tracking for K-12 Homeschooling parents
# HomeschoolHub - K-12 Learning App

A comprehensive mobile homeschool application with AI-generated lessons, interactive quizzes, and progress tracking for grades K-12.

## Features

### 📚 AI-Generated Lessons
- Pre-made lessons for Math, Science, English, and History
- Age-appropriate content for each grade level (K-12)
- Clear, engaging educational material

### ✅ Interactive Quizzes
- Multiple-choice quizzes after each lesson
- Immediate feedback on answers
- Score tracking and progress monitoring

### 🔒 Sequential Learning
- Lessons unlock progressively as students complete previous lessons
- Ensures structured learning path
- Prevents skipping ahead without mastering fundamentals

### 📊 Progress Tracking
- Comprehensive progress reports
- Track completed lessons and quiz scores
- View average performance across subjects
- Recent activity history

### 🎨 Modern UI
- Clean, intuitive interface designed for mobile
- Haptic feedback for interactions
- Dark mode support
- Colorful grade selection cards

## Getting Started

### Prerequisites
- Node.js 22+
- pnpm package manager
- MySQL database (provided by platform)

### Installation

1. Install dependencies:
```bash
pnpm install
```

2. Set up the database:
```bash
pnpm db:push
```

3. Seed sample lessons (optional):
```bash
npx tsx scripts/seed-sample-data.ts
```

4. Start the development server:
```bash
pnpm dev
```

5. Open the app:
   - **Web**: Navigate to the Metro URL shown in the terminal
   - **Mobile**: Scan the QR code with Expo Go app

## Project Structure

```
app/
  (tabs)/
    index.tsx          # Grade selection screen
    progress.tsx       # Progress tracking screen
  subjects.tsx         # Subject list for selected grade
  lessons.tsx          # Lesson list for selected subject
  lesson-content.tsx   # Individual lesson content
  quiz.tsx             # Quiz interface
  quiz-results.tsx     # Quiz results and scoring

server/
  routers.ts           # API endpoints (lessons, quizzes, progress)
  db.ts                # Database query helpers

drizzle/
  schema.ts            # Database schema (lessons, quizzes, progress)

components/
  screen-container.tsx # Safe area wrapper
  ui/                  # Reusable UI components
```

## Usage

### For Students

1. **Select Your Grade**: Choose from Kindergarten through Grade 12
2. **Pick a Subject**: Select Math, Science, English, or History
3. **Start Learning**: Read through the lesson content
4. **Take the Quiz**: Test your knowledge with 5 questions
5. **View Results**: See your score and unlock the next lesson
6. **Track Progress**: Check the Progress tab to see your achievements

### For Educators/Parents

- Monitor student progress through the Progress tab
- Review quiz scores and completion rates
- Identify areas where students may need additional support

## Generating New Lessons

To generate new lessons using AI:

```typescript
// Use the lessons.generate API endpoint
await trpc.lessons.generate.mutate({
  grade: "5",
  subject: "science",
  topic: "Solar System",
  orderIndex: 3,
});
```

The system will automatically:
1. Generate age-appropriate lesson content
2. Create a corresponding quiz with 5 questions
3. Add the lesson to the database

## Database Schema

### Lessons
- `id`: Unique identifier
- `grade`: K, 1-12
- `subject`: math, science, english, history
- `title`: Lesson title
- `content`: Lesson text content
- `orderIndex`: Sequential order within subject

### Quizzes
- `id`: Unique identifier
- `lessonId`: Associated lesson
- `questions`: JSON array of quiz questions

### Progress
- `id`: Unique identifier
- `lessonId`: Associated lesson
- `completed`: Boolean completion status
- `quizScore`: Number of correct answers
- `quizTotal`: Total number of questions
- `completedAt`: Timestamp

## Technology Stack

- **Frontend**: React Native with Expo SDK 54
- **Styling**: NativeWind (Tailwind CSS for React Native)
- **Backend**: Express + tRPC
- **Database**: MySQL with Drizzle ORM
- **AI**: Built-in LLM integration for content generation
- **State Management**: TanStack Query (React Query)

## Customization

### Adding New Subjects

Edit `app/subjects.tsx` and add to the `SUBJECTS` array:

```typescript
{ id: "art", name: "Art", icon: "book.fill" as const }
```

### Changing Colors

Update `theme.config.js` to customize the color palette:

```javascript
const themeColors = {
  primary: { light: '#1E40AF', dark: '#3B82F6' },
  // ... other colors
};
```

### Modifying Quiz Length

Edit `server/routers.ts` in the `quizzes.generate` mutation to change the number of questions.

## Sample Data

The app includes sample lessons for:
- Kindergarten Math: Counting to 10, Basic Shapes
- Grade 1 Math: Addition and Subtraction
- Grade 5 Science: The Water Cycle

Run the seed script to populate these:
```bash
npx tsx scripts/seed-sample-data.ts
```

## Deployment

1. Create a checkpoint:
```bash
# Make sure all changes are saved
```

2. Click the **Publish** button in the UI

3. Your app will be deployed and accessible via the provided URL

## Future Enhancements

- [ ] User authentication for multi-student households
- [ ] Lesson bookmarking and favorites
- [ ] Printable worksheets
- [ ] Parent dashboard with detailed analytics
- [ ] Gamification with badges and achievements
- [ ] Audio narration for lessons
- [ ] Offline mode support

## License

This project is created with Manus.

## Support

For questions or issues, visit [help.manus.im](https://help.manus.im)
