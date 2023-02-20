<template>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Roboto&display=swap" rel="stylesheet">
  <button id="stopAnimation">Start/Stop Animation</button>
  <main id="main">
    <div id="leftBar">
      <div id="leftBarContent">
        <h1>Start Studying Smarter!</h1>
        <p id="str"></p>
      </div>
      <form>
        <div class="leftBarSearch">
          <label for="universityInput">🎓 At which university do you study?</label>
          <input
              id="universityInput"
              v-model="searchValue"
              type="text"
              @focus="showList = true"
              @blur="showList = false"/>

          <ul v-if="showList && filteredCountries.length && searchValue !== ''">
            <li
                v-for="country in filteredCountries"
                v-on:mousedown="selectCountry(country)"
            >{{ country }}</li>
          </ul>
        </div>
        <div class="leftBarSearch">
          <label for="subjectInput">📚 Which subject do you study?</label>
          <input
              id="subjectInput"
              v-model="subjectValue"
              type="text"
              @focus="showSubjectList = true"
              @blur="showSubjectList = false"/>
          <ul v-if="showSubjectList && filteredSubjects.length && subjectValue !== '' ">
            <li
                v-for="subject in filteredSubjects"
                v-on:mousedown="selectSubject(subject)"
            >{{ subject }}</li>
          </ul>
        </div>
        <!-- <label for="universityInput">At which university do you study?</label> <br/>
                <input type="text" id="universityInput" placeholder="...">
                <label for="SubjectInput">Which subject do you study?</label> <br/>
                <input type="text" id="subjectInput" placeholder="...">-->
        <button type="submit">Find Flashcards</button>
      </form>
    </div>
    <div id="rightScroll">
      <div id="toolTip">
      <svg id="arrow" width="124" height="94" viewBox="0 0 186 141" fill="none" xmlns="http://www.w3.org/2000/svg">
        <g clip-path="url(#clip0_3_242)">
          <path d="M88.566 28.7352C85.5965 31.9046 81.5665 35.2852 78.8091 39.2996C73.0822 47.7512 67.7795 56.414 62.4768 65.0768C52.5077 81.5573 42.5387 98.2491 31.7212 116.209C45.7203 111.56 56.1135 99.7281 72.6579 102.475C71.1732 105.01 70.749 107.123 69.6885 107.546C53.1441 114.307 38.7207 124.449 25.1458 135.647C13.9041 144.733 8.1772 142.197 6.69244 128.463C5.20769 114.096 2.23823 99.7281 0.117153 85.3605C-0.307062 83.0363 0.541343 80.5009 0.75345 77.5428C9.87408 81.7686 9.87407 81.7686 17.5099 113.251C19.2068 110.504 20.6916 108.391 21.9642 106.278C34.4786 84.5154 46.7808 62.7527 59.7194 41.2012C63.9616 34.2287 69.0521 27.6788 74.779 21.974C84.9602 11.8322 96.2019 12.2547 105.747 23.0304C110.625 28.5239 114.231 35.2852 117.413 42.0464C121.019 49.6528 123.352 57.893 126.533 65.7107C128.867 71.2042 131.836 76.4864 134.593 82.1912C141.169 79.6557 143.714 74.7961 146.684 70.359C159.198 51.5544 168.531 31.482 175.53 9.93057C176.379 7.39511 176.803 4.64834 178.288 2.32417C179.136 1.05644 181.469 2.29715e-06 183.166 2.29715e-06C184.015 2.29715e-06 185.711 2.32418 185.923 3.59191C186.136 7.18382 185.923 11.1983 185.075 14.5789C179.136 38.8771 169.167 61.4849 154.956 81.9799C152.198 86.2057 148.593 90.0089 144.775 93.1782C137.775 98.883 130.775 98.6717 125.049 91.6992C120.382 85.9944 116.988 79.2332 114.019 72.4719C109.565 62.5414 106.383 52.1882 101.929 42.2577C99.3835 36.9755 96.414 31.482 88.566 28.7352Z" fill="#0D1927"/>
        </g>
        <defs>
          <clipPath id="clip0_3_242">
            <rect width="186" height="141" fill="white" transform="matrix(-1 0 0 -1 186 141)"/>
          </clipPath>
        </defs>
      </svg>
        <span>Click Me</span>
      </div>
      <Card></Card>
      <Card></Card>
      <Card></Card>
      <Card></Card>
      <Card></Card>
      <Card></Card>
    </div>

  </main>
</template>

<style scoped>

main {
  display: flex;
}

.searchLabel {
  display: flex;
  align-items: center;
  margin-top: 10px;
}

.leftBarSearch {
}

ul {
  background-color: white;
  padding: 0;
  margin: 0;
  list-style: none;
  position: absolute;
  max-height: 150px;
  overflow: auto;
  border: 4px #ccd8f8 solid;
  border-top: none;
  z-index: 2;
  margin-top: -7px;
  padding-bottom: 10px;
  width: 100%;
  box-sizing: border-box;
  border-bottom-right-radius: 10px;
  border-bottom-left-radius: 10px;
}

li {
  padding: 10px;
  cursor: pointer;
}
li:hover {
  background-color: lightgray;
}

@font-face {
  font-family: 'Pacifico';
  src: url('/Pacifico-Regular.ttf') format('truetype');
}

#toolTip {
  align-self: end;
  position: absolute;
  top: -80px;
  right: -10px;
  height: 150px;
  width: 400px;
  border-radius: 30px;
  display: flex;
  justify-content: center;
  text-align: center;
  transition: all 500ms ease;
  z-index: 1;
}

#toolTip span {
  margin: auto;
  font-size: 56px;
  display: inline-block;
  position: absolute;
  top: -30px;
  left: 80px;
  font-family: 'Pacifico', sans-serif !important;
  animation-name: appear;
  animation-timing-function: ease-in;
  animation-fill-mode: forwards;
  animation-iteration-count: 1;
  animation-duration: 1s;
  animation-delay: 2.7s;
  opacity: 0;
}


#arrow {
  align-self: end;
  position: absolute;
  left: 0;
  animation-name: appear;
  animation-timing-function: ease-in;
  animation-fill-mode: forwards;
  animation-iteration-count: 1;
  animation-duration: 1s;
  animation-delay: 2.5s;
  opacity: 0;
}

@keyframes appear {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

#leftBar {
  box-shadow: 30px 20px 30px -10px rgba(0, 0, 0, 0.3);
  width: 35%;
  height: 930px;
  border-bottom-right-radius: 30px;
  z-index: 1;
  background-color: white;
  margin-top: -130px;
  overflow-y: scroll;
  display: flex;
  flex-direction: column;
  align-content: center;
}

#leftBar::-webkit-scrollbar{
  display: none;
}

#leftBarContent {
  width: 80%;
  height: 100%;
  margin: auto;
  display: flex;
  flex-direction: column;
}

p {
  font-size: 28px;
  letter-spacing: 2px;
  text-align: justify;
  margin-bottom: 0;
}

h1 {
  font-size: 80px;
  margin-bottom: 0;
}

label {
  display: inline-block;
  margin-top: 20px;
  margin-bottom: 20px;
  font-size: 22px;
  font-weight: 700;
}

#leftBar input {
  border: 4px #ccd8f8 solid;
  border-radius: 10px;
  font-size: 16px;
  font-weight: 700;
  margin-top: -10px;
  height: 50px;
  width: 100%;
  box-sizing: border-box;
  background-color: #dee5fc;
  padding-left: 10px;
}

#leftBar input:focus {
  outline: none;
  transition: background-color 500ms;
  background-color: white;
}

#leftBar input:not(:focus) {
  transition: all 500ms;
}

form {
  display: flex;
  flex-direction: column;
  row-gap: 0;
  width: 80%;
  margin: auto;
  margin-bottom: 60px;
  position: relative;
}

form button {
  margin-top: 40px;
  background-color: black;
  border: none;
  color: white;
  font-size: 20px;
  border-radius: 10px;
  text-align: center;
  align-self: flex-end;
  padding: 15px 60px;
  font-weight: 700;
  /*box-shadow: rgba(0, 0, 0, 0.5) 0 5px 10px;*/
}

form button:hover {
  cursor: pointer;
  transition: all 400ms;
  /*transform: translateY(4px);*/
  scale: 105%;
}

form button:not(:hover) {
  transition: all 500ms;
}

#stopAnimation {
  align-self: end;
  position: absolute;
  top: 50px;
  right: 50px;
  visibility: hidden;
}

#rightScroll {
  position: relative;
  display: flex;
  flex-direction: row;
  width: 55%;
  margin-left: 100px;
  justify-content: space-around;
  align-content: space-around;
  flex-wrap: wrap;
  animation-duration: 3s;
  animation-delay: 1s;
  animation-timing-function: ease;
  animation-iteration-count: 1;
  animation-direction: normal;
  animation-play-state: running;
  animation-name: scroll;
  transform: translateX(-110%);
  animation-fill-mode: forwards;
}


/*
.hidden {
  opacity: 0;
  pointer-events: none;
}
*/

/* custom scrollbar */
ul::-webkit-scrollbar {
  width: 20px;
  height: 20px;
}

ul::-webkit-scrollbar-track {
  background-color: transparent;
}

ul::-webkit-scrollbar-thumb {
  background-color: #d6dee1;
  border-radius: 20px;
  border: 6px solid transparent;
  background-clip: content-box;
}

ul::-webkit-scrollbar-thumb:hover {
  background-color: #a8bbbf;
}



@keyframes scroll {
  0% {
    transform: translateX(-110%);
  }
  100% {
    animation-timing-function: ease-in;
    transform: translateX(0%);
  }
}



</style>


<script setup>

import Card from "../components/card";
import {onMounted} from "vue";
import { ref, computed } from 'vue';

const countries = ['Universität Wien', 'FH St. Pölten', 'Medizinische Universität Wien', 'Boku Wien', 'Universität für Angewandte Kunst Wien', 'Akademie der Bildenden Künste Wien', 'Harvard University', 'Stanford University', 'Princeton University', 'University of California, Los Angeles'];
/*const flashCards = {
  first: {
    subject: "Cognitive Psychology",

  }
}*/
const searchValue = ref('');
const showList = ref(false);

const filteredCountries = computed(() => {
  return countries.filter(country => country.toLowerCase().startsWith(searchValue.value.toLowerCase()));
});

function selectCountry(country) {
  searchValue.value = country
  showList.value = false;
}

const subjects = ['Accounting and Finance', 'Aeronautical and Manufacturing Engineering', 'Agriculture and Forestry',
'Anatomy and Physiology',
'Anthropology',
'Archaeology',
'Architecture',
'Art and Design',
'Biological Sciences',
'Building',
'Business and Management Studies',
'Chemical Engineering',
'Chemistry',
'Civil Engineering',
'Classics and Ancient History',
'Communication and Media Studies',
'Complementary Medicine',
'Computer Science',
'Counselling',
'Creative Writing',
'Criminology',
'Dentistry',
'Drama Dance and Cinematics',
'Economics',
'Education',
'Electrical and Electronic Engineering',
'English',
'Fashion',
'Film Making',
'Food Science',
'Forensic Science',
'General Engineering',
'Geography and Environmental Sciences',
'Geology',
'Health And Social Care',
'History',
'History of Art Architecture and Design',
'Hospitality Leisure Recreation and Tourism',
'Information Technology',
'Land and Property Management',
'Law',
'Linguistics',
'Marketing',
'Materials Technology',
'Mathematics',
'Mechanical Engineering',
'Medical Technology',
'Medicine',
'Music',
'Nursing',
'Occupational Therapy',
'Pharmacology and Pharmacy',
'Philosophy',
'Physics and Astronomy',
'Physiotherapy',
'Politics',
'Psychology',
'Robotics',
'Social Policy',
'Social Work',
'Sociology',
'Sports Science',
'Veterinary Medicine',
'Youth Work']
const subjectValue = ref('');
const showSubjectList = ref(false);

const filteredSubjects = computed(() => {
  return subjects.filter(subject => subject.toLowerCase().startsWith(subjectValue.value.toLowerCase()));
});

function selectSubject(subject) {
  subjectValue.value = subject
  /*showSubjectList.value = false;*/
}


onMounted(async () => {

  var string = "We've all been there, studying for university is a difficult task! Start relying on the proven success of the flashcards your peers have already created. This will save you precious time while improving short-term and long-term learning results!";
  var str = string.split("");
  var el = document.getElementById('str');
  (function animate() {
    str.length > 0 ? el.innerHTML += str.shift() : clearTimeout(running);
    var running = setTimeout(animate, 60);
  })();
});


</script>

<!--/*
// Stop Animation Button
const rightScroll = document.getElementById("rightScroll")
const stopAnimationButton = document.getElementById("stopAnimation")

stopAnimationButton.addEventListener("click", () => {
rightScroll.style.animationDuration === "0s" ? rightScroll.style.animationDuration = "8s" : rightScroll.style.animationDuration = "0s";
})

// Hide tooltip once the mouse enters #rightscroll
const toolTip = document.querySelector("#toolTip");

rightScroll.addEventListener("mouseenter", function() {
toolTip.classList.add("hidden");
});*/-->
