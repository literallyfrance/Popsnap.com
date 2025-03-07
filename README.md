import { useState } from "react";
import { BrowserRouter as Router, Route, Routes, Link, Navigate } from "react-router-dom";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";

function App() {
  const [user, setUser] = useState(null);
  return (
    <Router>
      <nav className="p-4 bg-blue-500 text-white flex justify-between">
        <h1 className="text-xl">PinClone</h1>
        <div>
          {!user ? (
            <Link to="/auth" className="mr-4">Login / Signup</Link>
          ) : (
            <Link to="/home">Home</Link>
          )}
        </div>
      </nav>
      <Routes>
        <Route path="/" element={<StartPage />} />
        <Route path="/auth" element={<AuthPage setUser={setUser} />} />
        <Route path="/home" element={user ? <HomePage user={user} /> : <Navigate to="/auth" />} />
      </Routes>
    </Router>
  );
}

function StartPage() {
  return (
    <div className="h-screen flex flex-col justify-center items-center">
      <h2 className="text-3xl mb-4">Welcome to PinClone</h2>
      <Link to="/auth">
        <Button>Get Started</Button>
      </Link>
    </div>
  );
}

function AuthPage({ setUser }) {
  const handleLogin = () => {
    setUser({ name: "User" });
  };
  return (
    <div className="h-screen flex flex-col justify-center items-center">
      <h2 className="text-2xl mb-4">Login or Create Account</h2>
      <Button onClick={handleLogin}>Login / Sign Up</Button>
    </div>
  );
}

function HomePage({ user }) {
  return (
    <div className="p-4">
      <h2 className="text-2xl mb-4">Welcome, {user.name}!</h2>
      <div className="grid grid-cols-3 gap-4">
        <Card>
          <CardContent>
            <img src="https://via.placeholder.com/200" alt="Sample" className="w-full" />
            <Button className="mt-2">Save</Button>
          </CardContent>
        </Card>
        {/* Add more images/videos dynamically */}
      </div>
    </div>
  );
}

export default App;
