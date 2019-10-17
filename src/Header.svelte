<div class="header-black">
        <div class="header-item"><a href="mailto:hamza.n.arshadwork@gmail.com" style="color: black">CONTACT</a></div>
        <div onclick="location.href = 'https://www.hamzaarshad.com/app/views/resume.html'" class="header-item">RESUME</div>
        <div onclick="location.href = 'https://www.hamzaarshad.com/app/views/portfolio.html'" class="header-item">PORTFOLIO</div>
        <div onclick="location.href = 'https://www.hamzaarshad.com/app/views/profile.html'" class="header-item">ABOUT</div>
        <div onclick="location.href = 'https://www.hamzaarshad.com'" class="header-item">HOME</div>
</div>

<style>
    .header-black {
        width: 100%;
        height: 100px;
        position: fixed;
        background-color: white;
        top: 0;
        left: 0;
        right: 0;
        font-family: 'Montserrat', sans-serif;
        font-weight: 300;
        color: black;
        z-index: 999;
        transition: all 0.2s linear;
    }
    .header-black.active{
        box-shadow: 0 0 10px rgba(0,0,0,0.4);
        background-color: white;
    }

    .logo-hna {
        width: 100px;
        margin-left: 10px;
        margin-top: 10px;
        cursor: pointer;
    }
    .header-item {
        float: right;
        margin-top: 40px;
        cursor:pointer;
        color:black;
        text-decoration: none;
        margin-right: 40px;
    }
</style>
