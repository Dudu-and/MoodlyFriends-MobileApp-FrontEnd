import { useState } from "react";
import { Send } from "lucide-react";

export default function ChatScreen() {
  const [messages, setMessages] = useState([
    { id: 1, sender: "outro", text: "Oi, tudo bem?" },
    { id: 2, sender: "eu", text: "Tudo sim, e você?" },
    { id: 3, sender: "outro", text: "Também! Bora estudar React?" },
  ]);
  const [input, setInput] = useState("");

  const handleSend = () => {
    if (input.trim() === "") return;
    setMessages([...messages, { id: Date.now(), sender: "eu", text: input }]);
    setInput("");
  };

  return (
    <div className="flex flex-col h-screen bg-gray-100">
      {/* Header */}
      <header className="bg-blue-600 text-white p-4 flex items-center justify-between shadow-md">
        <h1 className="text-lg font-semibold">Chat Principal</h1>
        <span className="text-sm opacity-80">Online</span>
      </header>

      {/* Lista de mensagens */}
      <div className="flex-1 overflow-y-auto p-4 space-y-3">
        {messages.map((msg) => (
          <div
            key={msg.id}
            className={`max-w-xs p-3 rounded-2xl shadow-sm ${
              msg.sender === "eu"
                ? "ml-auto bg-blue-500 text-white"
                : "mr-auto bg-white text-gray-800"
            }`}
          >
            {msg.text}
          </div>
        ))}
      </div>

      {/* Input fixo */}
      <div className="p-3 bg-white border-t flex items-center gap-2">
        <input
          type="text"
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="Digite sua mensagem..."
          className="flex-1 p-2 border rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
        <button
          onClick={handleSend}
          className="p-2 bg-blue-600 text-white rounded-xl hover:bg-blue-700 transition"
        >
          <Send size={20} />
        </button>
      </div>
    </div>
  );
}
