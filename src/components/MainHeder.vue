<template>
    <div class="header">
      <div class="logo">[לוגו האתר]</div>
      <div class="navigation">
        <button class="nav-button">בית</button>
        <button class="nav-button">מחשבון</button>
        <button class="nav-button">אודות</button>
        <button class="nav-button">צור קשר</button>
      </div>
    </div>
  </template>
  <script>
  export default {
    name: "MainHeder",
    props: {
      msg: String,
    },
  };
  </script>
  
  <style scoped>
  .header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #f0f0f0;
    padding: 10px;
  }
  
  .logo {
    font-size: 20px;
    font-weight: bold;
  }
  
  .navigation {
    display: flex;
  }
  
  .nav-button {
    background-color: transparent;
    border: none;
    margin: 0 10px;
    cursor: pointer;
  }
  
  .nav-button:hover {
    color: #ff0000; /* צבע כאשר מעבירים את העכבר מעל הכפתור */
  }
  </style>
  