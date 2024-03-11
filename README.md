const express = require("express");
const app = express();
const mongoose = require("mongoose");
const loginRouter = require("./routes/login.routes");

const path = require("path");
const cors = require("cors");
const dotenv = require('dotenv');
const https = require("https");
const fs =require("fs");
dotenv.config();

app.use(cors());
app.use(express.json());
app.use("/", loginRouter);
app.get("/",(req,res)=>{
  res.send("Bonjour tout le monde");
});
const options = {
  key:fs.readFileSync("./key.pem"),
  cert:fs.readFileSync("./cert.pem")
}

/*https.createServer(options,app)
  .listen(process.env.PORT, () => {
  console.log("Server running on port " + process.env.PORT);
  });*/

mongoose.connect(process.env.DB_URL)
.then(result => 
    https.createServer(options,app)
  .listen(process.env.PORT, () => {
  console.log("Server running on port " + process.env.PORT);
}))
.catch(error=>console.log(error));
