import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Progress } from "@/components/ui/progress";
import { CheckCircle } from "lucide-react";

const actions = [
  "Donate non-perishable food",
  "Give away clothes in good condition",
  "Help a classmate with homework",
  "Join a local clean-up day",
  "Share a social cause on your social media"
];

export default function ActuaHoy() {
  const [completed, setCompleted] = useState([]);

  const toggleAction = (index) => {
    setCompleted((prev) =>
      prev.includes(index)
        ? prev.filter((i) => i !== index)
        : [...prev, index]
    );
  };

  const progress = Math.round((completed.length / actions.length) * 100);

  return (
    <div className="min-h-screen bg-white text-gray-800 p-4 max-w-xl mx-auto">
      <h1 className="text-3xl font-bold text-center mb-6">Actúa Hoy</h1>
      <p className="text-center text-gray-600 mb-4">
        Small actions can make a big difference. Join the movement against poverty.
      </p>

      <div className="mb-6">
        <h2 className="text-xl font-semibold mb-2">Your Weekly Actions</h2>
        <Progress value={progress} className="mb-4" />
        <div className="space-y-3">
          {actions.map((action, index) => (
            <Card key={index} className="cursor-pointer" onClick={() => toggleAction(index)}>
              <CardContent className="flex items-center justify-between p-4">
                <span className={completed.includes(index) ? "line-through text-gray-400" : ""}> 
                  {action}
                </span>
                {completed.includes(index) && <CheckCircle className="text-green-500" />}
              </CardContent>
            </Card>
          ))}
        </div>
      </div>

      <div className="bg-blue-100 p-4 rounded-xl text-sm text-blue-800">
        <p><strong>Impact:</strong> {completed.length} of {actions.length} actions completed this week.</p>
        <p>Keep going! Every action helps someone in need.</p>
      </div>
    </div>
  );
}
