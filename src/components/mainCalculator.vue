<template>
  <!-- מסך ראשוני למחשבון -->
  <div id="Screen1" v-show="showScreen1">
    <h3>
      כמה דפים אני צריך לכתוב היום?
      <br />
      איך אני אמור לחשב כשיש לי חול המועד באמצע?
      <br />
      כמה תכלס אני מרוויח ביום על כתיבה?
      <br />
      רוצים לעשות סדר בכל הבלאגן?!
    </h3>
    <button @click="startCalculator">לחצו כאן להתחלת החישוב</button>
  </div>
  <!-- מסך שני למחשבון -->
  <div id="Screen2" v-show="showScreen2">
    <form id="fromScreen2">
      <fieldset>
        <legend>בחר סוג פרויקט</legend>

        <!-- אזור בחירת סוג ספר -->
        <div id="selctBook">
          <input
            type="radio"
            id="SeferTorah"
            name="item1"
            value="SeferTorah"
            v-model="userData.book"
            required
          />
          <label for="SeferTorah">ספר תורה</label>
          <input
            type="radio"
            id="Tfilin"
            name="item1"
            value="Tfilin"
            v-model="userData.book"
            required
          />
          <label for="Tfilin">תפילין</label>
          <input
            type="radio"
            id="Mezuzot"
            name="item1"
            value="Mezuzot"
            v-model="userData.book"
            required
          />
          <label for="Mezuzot">מזוזות</label>
          <input
            type="radio"
            id="MegilatEster"
            name="item1"
            value="MegilatEster"
            v-model="userData.book"
            required
          />
          <label for="MegilatEster">מגילת אסתר</label>
          <input
            type="radio"
            id="SeferHaftarot"
            name="item1"
            value="SeferHaftarot"
            v-model="userData.book"
            required
          />
          <label for="SeferHaftarot">ספר הפטרות</label>
          <input
            type="radio"
            id="Other"
            name="item1"
            value="Other"
            v-model="userData.book"
            required
          />
          <label for="Other">אחר</label>

          <hr />
        </div>
        <!-- אזור בחירת נתונים נוספים -->
        <label for="Amount"> הזן כמות </label>
        <input type="number" id="Amount" v-model="userData.info.AmountSelct" />
        <label for="date"> תאריך הגשה </label>
        <input type="date" id="date" v-model="userData.info.dateSelct" />
        <label for="profit"> רווח משוער </label>
        <input type="number" id="profit" v-model="userData.info.profitSelct" />
        <br />

        <label for="pages"> מספר עמודים (לספר 1) </label>
        <input type="number" id="pages" v-model="userData.info.pagesSelct" />
        <label for="workHours">שעות עבודה ליום </label>
        <input
          type="number"
          id="workHours"
          v-model="userData.info.workHoursSelct"
        />
        <hr />

        <!-- הזנת ימי עבודה בשבוע -->
        <h3>ימי עבודה בשבוע</h3>
        <input
          type="checkbox"
          id="workDay1"
          name="workDays"
          value="sunday"
          v-model="userData.workDays"
        />
        <label for="workDay1">יום ראשון</label>
        <input
          type="checkbox"
          id="workDay2"
          name="workDays"
          value="monday"
          v-model="userData.workDays"
        />
        <label for="workDay2">יום שני</label>
        <input
          type="checkbox"
          id="workDay3"
          name="workDays"
          value="tuesday"
          v-model="userData.workDays"
        />
        <label for="workDay3">יום שלישי</label>
        <input
          type="checkbox"
          id="workDay4"
          name="workDays"
          value="wednesday"
          v-model="userData.workDays"
        />
        <label for="workDay4">יום רביעי</label>
        <input
          type="checkbox"
          id="workDay5"
          name="workDays"
          value="thursday"
          v-model="userData.workDays"
        />
        <label for="workDay5">יום חמישי</label>
        <input
          type="checkbox"
          id="workDay6"
          name="workDays"
          value="friday"
          v-model="userData.workDays"
        />
        <label for="workDay6">יום שישי</label>
        <input
          type="checkbox"
          id="workDay7"
          name="workDays"
          value="saturday"
          v-model="userData.workDays"
        />
        <label for="workDay7">מוצאי שבת</label>
      </fieldset>
    </form>
    <button @click="startCalculator">חזור לשלב קודם</button>
    <button @click="submitScreen2">סיים וחשב</button>
  </div>
  <!-- מסך שלישי למחשבון -->
  <div v-show="showScreen3">
    <h1>התוצאה היא</h1>
    <h3>נתרו לך {{ calculatData.timeLeft }} ימי עבודה</h3>
    <h3>אתה צריך לכתוב {{ calculatData.pagePerDay }} דפים ליום</h3>
    <h3>הרווח המשוער הוא  {{ calculatData.profitPerDay }} שקלים ליום</h3>
    <h3>אתה צריך לכתוב {{ calculatData.writePagePerHour }} דפים לשעה</h3>
    <button @click="startCalculator">חישוב חדש</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //הגדרת תצוגת מסכים
      showScreen1: true,
      showScreen2: false,
      showScreen3: false,

      userData: {
        book: [],
        info: {
          AmountSelct: "",
          dateSelct: "",
          profitSelct: "",
          pagesSelct: "",
          workHoursSelct: "",
        },
        workDays: [],
      },
      saveData: [],
      calculatData: {
        nowTimeMs: "",
        totalWorkDay: 0,
        timeLeft: 0,
        pagePerDay: 0,
        profitPerDay: 0,
        writePagePerHour: 0,
      },
    };
  },
  methods: {
    //פתיחת טופס המחשבון
    startCalculator() {
      this.showScreen1 = !this.showScreen1;
      this.showScreen2 = !this.showScreen2;
    },
    //ביצוע פעולות החישוב והצגת התוצאה
    submitScreen2() {
      this.showScreen2 = !this.showScreen2;
      this.showScreen3 = !this.showScreen3;
      this.saveData.push({ ...this.userData });

      this.dayCalc(); //הפעלת פונקציה לחישוב ימי עבודה שנתרו
      this.pagsPerDay(); // הפעלת פונקציית חישוב כמות הדפים ליום
      this.profitPerDay(); //הפעלת פונקציית חישוב רווח ליום
      this.writePage()  //הפעלת פונקציית חישוב קצב כתיבה נדרש
    },

    //חישוב ימי עבודה
    dayCalc() {
      const dateUser = new Date(this.saveData[0].info.dateSelct);
      const today = new Date();
      let workDaysLeft = 0;
      while (today <= dateUser) {
        if (
          this.userData.workDays.includes(
            today.toLocaleDateString("en-US", { weekday: "long" }).toLowerCase()
          )
        ) {
          workDaysLeft++;
        }
        today.setDate(today.getDate() + 1); //נצרך כיוון שמחשב הימים מ0
      }
      this.calculatData.timeLeft = workDaysLeft;
      console.log(this.userData.workDays);
    },

    //חישוב כמות הדפים ליום עבודה
    pagsPerDay() {
      let pegs =
        (this.userData.info.AmountSelct * this.userData.info.pagesSelct) /
        this.calculatData.timeLeft;
      this.calculatData.pagePerDay = pegs;
    },
    //חישוב רווח משוער ליום עבודה
    profitPerDay() {
      let profit =
        this.userData.info.profitSelct  /
        this.calculatData.timeLeft;
      this.calculatData.profitPerDay = profit;
    },
    //חישוב קצב כתיבה לדף
    writePage() {
      let writePage = this.calculatData.pagePerDay / this.userData.info.workHoursSelct;
      this.calculatData.writePagePerHour = writePage;
    },
  },
  mounted() {
    const dateZero = new Date();
    this.calculatData.nowTimeMs = dateZero;
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  color: #333;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

/* עיצוב למסך הראשון */
#Screen1 {
  text-align: center;
  padding: 50px;
}

#Screen1 h3 {
  font-size: 24px;
  line-height: 1.5;
}

#Screen1 button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 10px 20px;
  font-size: 18px;
  cursor: pointer;
}

#Screen1 button:hover {
  background-color: #0056b3;
}

/* עיצוב למסך השני */
#Screen2 {
  margin-top: 50px;
}

#Screen2 form {
  background-color: #fff;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

#Screen2 fieldset {
  border: none;
  margin: 0;
  padding: 0;
}

#Screen2 legend {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
}

#Screen2 label {
  margin-bottom: 10px;
}

#Screen2 input[type="radio"] {
  margin-right: 5px;
}

#Screen2 input[type="number"],
#Screen2 input[type="date"] {
  width: 100%;
  padding: 5px;
  border-radius: 3px;
  border: 1px solid #ccc;
}

#Screen2 button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 10px 20px;
  font-size: 18px;
  cursor: pointer;
  margin-top: 10px;
  margin: 10px;
}

#Screen2 button:first-child {
  margin-right: 10px;
}

#Screen2 button:hover {
  background-color: #0056b3;
}

/* עיצוב למסך השלישי */
#Screen3 {
  margin-top: 50px;
}
</style>