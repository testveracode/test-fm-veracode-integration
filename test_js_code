// app.js
const express = require("express");
const { exec } = require("child_process");
const fs = require("fs");

const app = express();
app.use(express.json());

// Hardcoded secret - for SAST testing
const API_KEY = "12345-SECRET-KEY";

// Command Injection vulnerability
app.get("/ping", (req, res) => {
  const host = req.query.host;
  exec("ping -c 1 " + host, (err, stdout, stderr) => {
    if (err) return res.status(500).send(stderr);
    res.send(stdout);
  });
});

// Path Traversal vulnerability
app.get("/file", (req, res) => {
  const fileName = req.query.name;
  const data = fs.readFileSync("./files/" + fileName, "utf8");
  res.send(data);
});

// Insecure logging
app.post("/login", (req, res) => {
  console.log("Login request:", req.body);
  res.send({
    message: "Logged in",
    token: API_KEY
  });
});

app.listen(3000, () => {
  console.log("Vulnerable test app running on http://localhost:3000");
});
