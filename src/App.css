import React, { useState, useEffect } from "react";
import Calendar from "react-calendar";
import "react-calendar/dist/Calendar.css";
import "./App.css"; // optional if you want extra styles

const defaultTasks = [
  "Exercise",
  "Read",
  "Meditate",
  "Work on project",
];

function App() {
  const [selectedDate, setSelectedDate] = useState(new Date());
  const [tasksByDate, setTasksByDate] = useState({});

  // Load saved tasks from localStorage
  useEffect(() => {
    const saved = localStorage.getItem("tasksByDate");
    if (saved) setTasksByDate(JSON.parse(saved));
  }, []);

  // Save tasks whenever tasksByDate changes
  useEffect(() => {
    localStorage.setItem("tasksByDate", JSON.stringify(tasksByDate));
  }, [tasksByDate]);

  const handleTaskChange = (task) => {
    const dateKey = selectedDate.toDateString();
    const currentTasks = tasksByDate[dateKey] || {};
    setTasksByDate({
      ...tasksByDate,
      [dateKey]: {
        ...currentTasks,
        [task]: !currentTasks[task],
      },
    });
  };

  const countCompletedTasks = (date) => {
    const tasks = tasksByDate[date.toDateString()];
    if (!tasks) return 0;
    return Object.values(tasks).filter(Boolean).length;
  };

  const getDayColor = (date) => {
    const completed = countCompletedTasks(date);
    const total = defaultTasks.length;
    if (completed === 0) return "#eee";
    if (completed < total) return "#f7d794"; // partial
    return "#78e08f"; // all completed
  };

  return (
    <div className="min-h-screen flex flex-col items-center justify-start p-6 bg-gray-100">
      <h1 className="text-3xl font-bold mb-4">Consistency Tracker</h1>
      <Calendar
        onChange={setSelectedDate}
        value={selectedDate}
        tileContent={({ date, view }) => {
          if (view === "month") {
            const color = getDayColor(date);
            return (
              <div
                style={{
                  backgroundColor: color,
                  borderRadius: "50%",
                  width: "20px",
                  height: "20px",
                  margin: "0 auto",
                  marginTop: "4px",
                }}
              ></div>
            );
          }
        }}
      />

      <h2 className="text-xl font-semibold mt-6 mb-2">
        Tasks for {selectedDate.toDateString()}
      </h2>

      <div className="flex flex-col gap-2">
        {defaultTasks.map((task) => (
          <label key={task} className="flex items-center gap-2">
            <input
              type="checkbox"
              checked={
                tasksByDate[selectedDate.toDateString()]
                  ? tasksByDate[selectedDate.toDateString()][task] || false
                  : false
              }
              onChange={() => handleTaskChange(task)}
            />
            {task}
          </label>
        ))}
      </div>
    </div>
  );
}

export default App;
