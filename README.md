# Weather-app-
//html code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>Weather App</h1>
        <form action="#">
            <input id="city name" type="text" placeholder="Enter your city name">
            <input type="submit" value="Get weather">
        </form>
        <div class="weather-data">
            <div class="icon">
                <!--<img src="https://openweathermap.org/img/wn/01d.png" alt="">-->
            </div>
            <div class="temp"></div>
            <div class="descp"></div>
            <!--<div class="temp">35°C</div>
            <div class="descp">haze</div>-->
            <div class="details">
                <!--<div>Feels Like: 35°C</div>
                <div>Humidity: 45%</div>
                <div> Wind Speed: 5 m/s</div>-->
                <div></div>
                <div></div>
                <div></div>
            </div>
        </div>
    </div>
    <script src ="script.js"></script>
</body>
</html>
// css code
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: cursive;
}
body{ 
    background-color:#96bdc6;
}
.container{
    background-color:#e0dddd;
    max-width: 600px;
    text-align: center;
    padding: 20px;
    box-shadow: 10px 10px 20px rgba(0,0,0,0.6);
    margin: 20px auto;
    margin-top: 40px;
    border-radius: 10px;
}
form{
    display: flex;
    justify-content:center;
    margin: 30px;   
}
form input[type="text"]{
    padding: 10px;
    font-size: 18px;
    width: 70%;
    border: none;
    outline: none;
    border-radius: 5px;
}
form input[type="submit"]{
    padding: 10px 20px;
    border: none;
    background-color:#e32417d3;
    color:white;
    font-size: 18px;
    border-radius: 5px;
    cursor: pointer;
    transition: all 0.2s ease-in;
}form input[type="submit"]:hover{
    background-color: rgb(171,75,75);
}
.icon img{
    width: 100px;
    height: 100px;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center center;
}
.temp{
    font-size: 40px;
    font-weight:900;
    margin-top:10px;
}
.descp{
    font-size: 30px;
    font-weight: 600;
    margin-top: 5px;
    margin-bottom:10px;
}
.details{
    display:flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap:wrap;
}
.details>div{
    font-size:18px;
    background-color: antiquewhite;
    padding:20px;
    border-radius:5px;
    margin:10px;
    text-align:center;
    align-items: center;
    flex:1;
    
}
//Javascript code
const apiKey ="0f9c4737da933c6ad51a7139fb262bfb"
const weatherDataEle = document.querySelector(".weather-data")
const cityNameEle = document.querySelector("#city-name")
const formEle = document.querySelector("form")
const imgIcon = document.querySelector(".icon")
formEle.addEventListener("submit",(e)=>{
    e.preventDefault()
    //console.log(cityNameEle.value);
    const cityValue = cityNameEle.value

    getWeatherData(cityValue)
})

async function  getWeatherData(cityValue){
    try{
        const response = await fetch
        (https://api.openweathermap.org/data/2.5/weather?q=${cityValue}&appid=${apiKey}&units=metric)
        if(!response.ok){
            throw new Error("Network response is not ok!")
        }
        const data = await response.json()
        //console.log(data);

        const temprature = Math.floor(data.main.temp)
        const description  = data.weather[0].description
        const icon  = data.weather[0].icon
        
        const details = [
            Feels Like: ${Math.floor(data.main.feels_like)}°C,
            Humidity:${data.main.humidity}%,
            Wind Speed: ${data.wind.speed}m/s
        ]
         weatherDataEle.querySelector(".temp").textContent = ${temprature}°C
         weatherDataEle.querySelector(".descp").textContent = ${description}

         imgIcon.innerHTML = <img src = "https://openweathermap.org/img/wn/${icon}.png" alt="">

         weatherDataEle.querySelector(".details").innerHTML = details.map((detail)=>{
            return <div>${detail}</div>
         }).join("")
    }
    catch(err){
        weatherDataEle.querySelector(".temp").textContent = ""
        imgIcon.innerHTML = ""
         weatherDataEle.querySelector(".descp").textContent = " An Error Occurred!"
    }
}
