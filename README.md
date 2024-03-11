const express = require("express");
const cors = require("cors");
const axios = require('axios')
const app = express();
app.use(cors());
app.use(express.json());

    
  app.post('/validate_captcha',async (req,res)=>{
    const captchaValue  = req.body.captchaValue
    const SECRET_KEY='6LfJuYQpAAAAAFvOwBInMKSFamS9IA0Ao4vTRLA2';
    const {data}  = await axios.post(
      `https://www.google.com/recaptcha/api/siteverify?secret=${SECRET_KEY}&response=${captchaValue}`,
    )
    console.log(data);
    res.status(200).json(data);
})

app.listen(5000,()=>{
  console.log("server running");
});
