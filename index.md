<!DOCTYPE html>
<html>
	<head>
		<title>Bio Lord's Journey</title>
		<meta charset = "UTF-8">
		<link rel="stylesheet" type="text/css" href="Game Page.css">
		<link rel="icon" href="favicon.png" type="image/gif">
		<link href='https://fonts.googleapis.com/css?family=Slackey' rel='stylesheet'>
		<link href='https://fonts.googleapis.com/css?family=Sofadi One' rel='stylesheet'>
		<link href='https://fonts.googleapis.com/css?family=Stardos Stencil' rel='stylesheet'>
	</head>
	<body id="body">
		<div id="container">
			<div id="left">
				<div id="blank">
					<h2 id="difficulty"></h2>
					<h3 id="quesNumber"></h3>
					<p id="question"></p>
					<div id="choices">
						<div id="up">
							<button id="choice1" onclick="highlight1()"></button>
							<button id="choice3" onclick="highlight3()"></button>
						</div>
						<div id="down">
							<button id="choice2" onclick="highlight2()"></button>
							<button id="choice4" onclick="highlight4()"></button>
						</div>
					</div>
				</div>
				<p id="comment" style="display: none"></p>
				<div id="inputContainer">
					<input id="inputAns" type="text" style="display: none"</input>
				</div>
				<button id="confirm" onclick="chooseAnswer(); dragAnimation()">Confirm</button>
				<button id="next" style="display: none" onclick="nextQues()">Next</button>
				
			</div>
			
			<div id="right">
				<div id="healthContainer">
					<div id="healthBar"></div>
				</div>
				<div id="animations">
					<div id="dragon"></div>
					<div id="knight"></div>
				</div>
			</div>
		</div>
		<script>
			let corAns, chosenquestion, check = 0, items = 0, quesNum = 1, p = 0, numChoice = [], difficulty = "Zoratia", choice = 0, wrong = false, currHealth = 100, subt = 0;
			
			alert("Welcome Bio Lord! As you may know, our kingdom is being terrorized by an evil dragon. In line with this, our king has sent you on a journey to find a new land for our people. Do know that this journey will not be easy. The dragon will do its best to try and stop you. Bio Lord, you must succeed!");
			
			function newQues() {

				let ques = ["What is the basic unit of life?", "Regarded as the Father of Microscopy", "What is the control center of the body?", "Organ that digests food", "What are the smallest blood vessel?"], 
				quesAve = ["Interstitial Fluid in Insects", "What drives the movement of water in the xylem?", "Body system responsible for transport and circulation.", "Type of immunity wherein an individual develops immunity after injection of  inactivated forms of pathogen into the body.", "Who pioneered vaccination?", "What do you call a complete digestive system?", "How many chambers does a ruminant's stomach have?", "Feeding mechanism used by fishes", "Functional units of the kidneys", "Respiratory pigment in humans that transports oxygen?"], 
				quesDiff = ["Biggest organ in the human body.", "Protein shell that encloses a virus.", "Who proposed the theory of evolution?", "Process by which cells engulf particles.", "Primary nitrogenous waste of humans."], count = 0, x = 0;
				
				document.getElementById('choice1').style.removeProperty("background-color");
				document.getElementById('choice2').style.removeProperty("background-color");
				document.getElementById('choice3').style.removeProperty("background-color");
				document.getElementById('choice4').style.removeProperty("background-color");
				document.getElementById('inputAns').style.removeProperty("background-color");
				document.getElementById('next').style.display = "none";
				document.getElementById('confirm').style.display = "block";
				
				if (items < 5) {
					x = 4;
					nques = ques;
					subt = 20;
					if (items == 0) {
						alert("You have arrived in Zoratia. This is the first place you have to go through in order to find a new land. To survive, you must answer 1 out of 5 questions correctly. Do not fret for the questions in this place are relatively easy. Goodluck!");
					}
				}
				else if (items > 4 && items < 15) {
					difficulty = "Lestavia";
					x = 9;
					nques = quesAve;
					if (items == 5) {
						subt = 25;
						currHealth = 100;
						document.getElementById('healthBar').style.width = "100%";
						document.getElementById('healthBar').style.backgroundColor = "green";
						p = 0;
						alert("Congratulations! You have survived your journey in Lestavia. However, do not rejoice yet for Lestavia was just the beginning. Now, you will have to pass through Golemia, the abode of the golems.");
						alert("In this round, you will have to answer 10 questions. To survive, you must get at least 7 correct answers. Goodluck Bio Lord!");
					}
				}
				else if (items > 14 && items < 20) {
					difficulty = "Draconia";
					x = 4;
					nques = quesDiff;
					document.getElementById('inputAns').value = "";
					
					if (items == 15) {
						subt = 30;
						currHealth = 100;
						document.getElementById('healthBar').style.width = "100%";
						document.getElementById('healthBar').style.backgroundColor = "green";
						p = 0;
						alert("You have reached the last place, Draconia, the home of the dragon itself. In this place, there will no longer be any choices. Answers must be typed. To survive, you must get at least 3 correct answers. Goodluck!");
						document.getElementById('choices').style.display = "none";
						document.getElementById('inputAns').style.display = "block";
						
					}
				}
				
				document.getElementById('difficulty').innerHTML = difficulty;
				document.getElementById('quesNumber').innerHTML = "Question " + quesNum;
				quesNum++;
				
				if (p == 0) {
					function randomNumber() {
						let numSet = [];
						
						for (i = 0; i <= x; i++) {
							let check = true;
								while (check) {
									let rand = Math.round(Math.random() * x);
									check = numSet.includes(rand);
								
									if (check == false) {
										numSet.push(rand);
									}
								}
							}
						return numSet;
					}
					numChoice = randomNumber();
				}
				
				function randomQuestion() { 
					let question = nques[numChoice[p]];
					document.getElementById('question').innerHTML = question ;
					return question;
				}
					
				chosenquestion = randomQuestion();
				
				//Easy questions
				if (chosenquestion == "What is the basic unit of life?") {
					document.getElementById('choice1').innerHTML = "a. Cell";
					document.getElementById('choice2').innerHTML = "b. Virus";
					document.getElementById('choice3').innerHTML = "c. Blood";
					document.getElementById('choice4').innerHTML = "d. Bacteria";
					corAns = "a";
				}
				if (chosenquestion == "Regarded as the Father of Microscopy") {
					document.getElementById('choice1').innerHTML = "a. Alexander Graham Bell";
					document.getElementById('choice2').innerHTML = "b. Antonie van Leeuwenhoek";
					document.getElementById('choice3').innerHTML = "c. Thomas Edison";
					document.getElementById('choice4').innerHTML = "d. Charles Darwin";
					corAns = "b";
				}
				if (chosenquestion == "What is the control center of the body?") {
					document.getElementById('choice1').innerHTML = "a. Heart";
					document.getElementById('choice2').innerHTML = "b. Brain";
					document.getElementById('choice3').innerHTML = "c. Skin";
					document.getElementById('choice4').innerHTML = "d. Lungs";
					corAns = "b";
				}
				if (chosenquestion == "Organ that digests food") {
					document.getElementById('choice1').innerHTML = "a. Stomach";
					document.getElementById('choice2').innerHTML = "b. Skin";
					document.getElementById('choice3').innerHTML = "c. Heart";
					document.getElementById('choice4').innerHTML = "d. Liver";
					corAns = "a";
				}
				if (chosenquestion == "What are the smallest blood vessel?") {
					document.getElementById('choice1').innerHTML = "a. Veins";
					document.getElementById('choice2').innerHTML = "b. Arteries";
					document.getElementById('choice3').innerHTML = "c. Arterioles";
					document.getElementById('choice4').innerHTML = "d. Capillaries";
					corAns = "d";
				}
				//Average questions
				if (chosenquestion == "Interstitial Fluid in Insects") {
					document.getElementById('choice1').innerHTML = "a. Water";
					document.getElementById('choice2').innerHTML = "b. Oxygen";
					document.getElementById('choice3').innerHTML = "c. Hemolymph";
					document.getElementById('choice4').innerHTML = "d. Blood";
					corAns = "c";
				}
				if (chosenquestion == "What drives the movement of water in the xylem?") { 
					document.getElementById('choice1').innerHTML = "a. Countercurrent exchange";
					document.getElementById('choice2').innerHTML = "b. Liquefaction";
					document.getElementById('choice3').innerHTML = "c. Evaporation";
					document.getElementById('choice4').innerHTML = "d. Transpiration";
					corAns = "d";
				}
				if (chosenquestion == "Body system responsible for transport and circulation.") {
					document.getElementById('choice1').innerHTML = "a. Urinary System";
					document.getElementById('choice2').innerHTML = "b. Circulatory System";
					document.getElementById('choice3').innerHTML = "c. Integumentary System";
					document.getElementById('choice4').innerHTML = "d. Immune System";
					corAns = "b";
				}
				if (chosenquestion == "Type of immunity wherein an individual develops immunity after injection of  inactivated forms of pathogen into the body.") {
					document.getElementById('choice1').innerHTML = "a. Natural Passive Immunity";
					document.getElementById('choice2').innerHTML = "b. Artificial Active Immunity";
					document.getElementById('choice3').innerHTML = "c. Artificial Passive Immunity";
					document.getElementById('choice4').innerHTML = "d. Natural Active Immunity";
					corAns = "b";
				}
				if (chosenquestion == "Who pioneered vaccination?") {
					document.getElementById('choice1').innerHTML = "a. Edward Jenner";
					document.getElementById('choice2').innerHTML = "b. Louis Pastuer";
					document.getElementById('choice3').innerHTML = "c. Zacharias Janssen";
					document.getElementById('choice4').innerHTML = "d. Albert Einstein";
					corAns = "a";
				}
				if (chosenquestion == "What do you call a complete digestive system?") {
					document.getElementById('choice1').innerHTML = "a. Digestive Tract";
					document.getElementById('choice2').innerHTML = "b. Esophagus";
					document.getElementById('choice3').innerHTML = "c. Alimentary Canal";
					document.getElementById('choice4').innerHTML = "d. Gastrovascular Cavity";
					corAns = "c";
				}
				if (chosenquestion == "How many chambers does a ruminant's stomach have?") { 
					document.getElementById('choice1').innerHTML = "a. 1";
					document.getElementById('choice2').innerHTML = "b. 2";
					document.getElementById('choice3').innerHTML = "c. 3";
					document.getElementById('choice4').innerHTML = "d. 4";
					corAns = "d";
				}
				if (chosenquestion == "Feeding mechanism used by fishes") { 
					document.getElementById('choice1').innerHTML = "a. Fluid Feeding";
					document.getElementById('choice2').innerHTML = "b. Substrate Feeding";
					document.getElementById('choice3').innerHTML = "c. Suspension Feeding";
					document.getElementById('choice4').innerHTML = "d. Bulk Feeding";
					corAns = "c";
				}
				if (chosenquestion == "Functional units of the kidneys") { 
					document.getElementById('choice1').innerHTML = "a. Neurons";
					document.getElementById('choice2').innerHTML = "b. Lobule";
					document.getElementById('choice3').innerHTML = "c. Nerves";
					document.getElementById('choice4').innerHTML = "d. Nephrons";
					corAns = "d";
				}
				if (chosenquestion == "Respiratory pigment in humans that transports oxygen?") {
					document.getElementById('choice1').innerHTML = "a. Hemoglobin";
					document.getElementById('choice2').innerHTML = "b. Hemocyanin";
					document.getElementById('choice3').innerHTML = "c. Hemerythrin";
					document.getElementById('choice4').innerHTML = "d. Chlorocruorin";
					corAns = "a";
				}
				//Difficult questions
				if (chosenquestion == "Biggest organ in the human body.") {
					corAns = "skin";
				}
				if (chosenquestion == "Protein shell that encloses a virus.") {
					corAns = "capsid";
				}
				if (chosenquestion == "Who proposed the theory of evolution?") {
					corAns = "charles darwin";
				}
				if (chosenquestion == "Process by which cells engulf particles.") {
					corAns = "phagocytosis";
				}
				if (chosenquestion == "Primary nitrogenous waste of humans.") {
					corAns = "urea";
				}
				p++;
			}	
			
			function highlight1() {
				document.getElementById('choice1').style.backgroundColor = "gray";
				document.getElementById('choice2').style.removeProperty("background-color");
				document.getElementById('choice3').style.removeProperty("background-color");
				document.getElementById('choice4').style.removeProperty("background-color");
				choice = 1;
			}
			function highlight2() {
				document.getElementById('choice2').style.backgroundColor = "gray";
				document.getElementById('choice1').style.removeProperty("background-color");
				document.getElementById('choice3').style.removeProperty("background-color");
				document.getElementById('choice4').style.removeProperty("background-color");
				choice = 2;
			}
			function highlight3() {
				document.getElementById('choice3').style.backgroundColor = "gray";
				document.getElementById('choice1').style.removeProperty("background-color");
				document.getElementById('choice2').style.removeProperty("background-color");
				document.getElementById('choice4').style.removeProperty("background-color");
				choice = 3;
			}
			function highlight4() {
				document.getElementById('choice4').style.backgroundColor = "gray";
				document.getElementById('choice1').style.removeProperty("background-color");
				document.getElementById('choice2').style.removeProperty("background-color");
				document.getElementById('choice3').style.removeProperty("background-color");
				choice = 4;
			}
			
			function chooseAnswer() {
				if (choice == 1) {
					check1();
				}
				if (choice == 2) {
					check2();
				}
				if (choice == 3) {
					check3();
				}
				if (choice == 4) {
					check4();
				}
				if (choice == 1 || choice == 2 || choice == 3 || choice == 4) {
				document.getElementById('next').style.display = "inline";
				document.getElementById('confirm').style.display = "none";
				}
			
				
				if (difficulty == "Draconia") {
					ans = document.getElementById('inputAns').value;
					
					let x = corAns.charAt(0);
					let y = x.toUpperCase();
					let z = corAns.replace(corAns.charAt(0), y);
					
					if  (items == 19) {
						check++;
						document.getElementById('body').style.background = "url('lastbg.JPG')";
						document.getElementById('blank').innerHTML = "You got " + check + " out of 20";
						document.getElementById('blank').style.fontSize = "xx-large";
						document.getElementById('blank').style.paddingBottom = "10%";
						document.getElementById('blank').style.paddingBottom = "0";
						document.getElementById('confirm').style.display = "none";
						document.getElementById('next').style.display = "inline";
						document.getElementById('next').setAttribute("onClick", "homePage()");
						document.getElementById('next').innerHTML = "Home";
						document.getElementById('comment').style.display = "block";
						document.getElementById('inputContainer').style.display = "none";
						document.getElementById('right').style.display = "none";
						document.getElementById('left').style.float = "none";
						document.getElementById('left').style.width = "100%";
						document.getElementById('comment').innerHTML = "Hooray! You have saved the kingdom! The king has abdicated. You are now the Bio King. Congratulations!";
					}
					
					if (ans == corAns || ans == z || ans == corAns.toUpperCase() || ans == "Charles Darwin" || ans == "charles Darwin") {
						document.getElementById('inputAns').style.backgroundColor = "green";
						document.getElementById('next').style.display = "inline";
						document.getElementById('confirm').style.display = "none";
						check++;
						items++;
						wrong = false();
						newQues();
					}	
					
					else {
						document.getElementById('inputAns').style.backgroundColor = "red";
						document.getElementById('next').style.display = "inline";
						document.getElementById('confirm').style.display = "none";
						wrong = true;
						items++;
					}
				}
			}
			
			function check1() {
				if (chosenquestion == "What is the basic unit of life?" || chosenquestion == "Organ that digests food" || chosenquestion == "Who pioneered vaccination?" || chosenquestion == "Respiratory pigment in humans that transports oxygen?") {
					document.getElementById('choice1').style.backgroundColor = "green";
					check++;
					items++;
				}
				else {
					document.getElementById('choice1').style.backgroundColor = "red";
					wrong = true;
					items++;
				}
			}
			function check2() {
				if (chosenquestion == "Regarded as the Father of Microscopy" || chosenquestion == "What is the control center of the body?" || chosenquestion == "Body system responsible for transport and circulation." || chosenquestion == "Type of immunity wherein an individual develops immunity after injection of  inactivated forms of pathogen into the body.") {
					document.getElementById('choice2').style.backgroundColor = "green";
					check++;
					items++;
				}
				else {
					document.getElementById('choice2').style.backgroundColor = "red";
					wrong = true;
					items++;
				}
			}
			function check3() {
				if (chosenquestion == "Interstitial Fluid in Insects" || chosenquestion == "What do you call a complete digestive system?" || chosenquestion == "Feeding mechanism used by fishes") {
					document.getElementById('choice3').style.backgroundColor = "green";
					check++;
					items++;
				}
				else {
					document.getElementById('choice3').style.backgroundColor = "red";
					wrong = true;
					items++;
				}
			}
			function check4() {
				if (chosenquestion == "What are the smallest blood vessel?" || chosenquestion == "What drives the movement of water in the xylem?" || chosenquestion == "How many chambers does a ruminant's stomach have?" || chosenquestion == "Functional units of the kidneys") {
					document.getElementById('choice4').style.backgroundColor = "green";
					check++;
					items++;
				}
				else {
					document.getElementById('choice4').style.backgroundColor = "red";
					wrong = true;
					items++;
				}
			}
			
			function dragAnimation() {
				let land = 0, wings = 0, flight = 0;
				
				if (wrong == false) {
					land = setInterval(drag1, 400);
					wings = setInterval(drag2, 800);
					flight = setInterval(drag3, 1200);
				}
				else if (wrong == true) {
					clearInterval(land);
					const breath = setTimeout(dragBreath, 100);
				}
				
				function drag1() {
					document.getElementById('dragon').style.background = "url(dragon.png) no-repeat -8px -258px"
					document.getElementById('dragon').style.width = "148px";
					document.getElementById('dragon').style.height = "167px";
				}
				function drag2() {
					document.getElementById('dragon').style.background = "url(dragon.png) no-repeat -196px -251px ";
					document.getElementById('dragon').style.width = "152px";
					document.getElementById('dragon').style.height = "167px";
				}
				function drag3() {
					document.getElementById('dragon').style.background = "url(dragon.png) no-repeat -387px -213px"
					document.getElementById('dragon').style.width = "147px";
					document.getElementById('dragon').style.height = "167px";
				}
				function dragBreath() {
					currHealth = currHealth - subt;
					
					document.getElementById('dragon').style.background = "url(dragon.png) no-repeat -263px -18px"
					document.getElementById('dragon').style.width = "275px";
					document.getElementById('dragon').style.height = "167px";
					
					
					if (currHealth > 60) {
						document.getElementById('healthBar').style.width = currHealth + "%";
					}
					if (currHealth <= 60) {
						document.getElementById('healthBar').style.backgroundColor = "yellow";
						document.getElementById('healthBar').style.width = currHealth + "%";
					}
					if (currHealth <= 30) {
						document.getElementById('healthBar').style.backgroundColor = "red";
						document.getElementById('healthBar').style.width = currHealth + "%";
					}
					if (currHealth <= 0) {
						document.getElementById('left').style.width = "100%";
						document.getElementById('right').style.display = "none";
						document.getElementById('blank').innerHTML = "YOU DIED";
						document.getElementById('blank').style.fontSize = "50px";
						document.getElementById('next').setAttribute("onClick", "homePage()");
						document.getElementById('next').innerHTML = "Retry";
						document.getElementById('inputContainer').style.display = "none";
					}
				}	
			}
			dragAnimation();
		
			function knightAnimation() {
				const idle = setInterval(knight1, 300);
				const stand = setInterval(knight2, 600);
				
				function knight1() {
					document.getElementById('knight').style.background = "url(knight.png) no-repeat -19px -21px"
					document.getElementById('knight').style.width = "61px";
					document.getElementById('knight').style.height = "44px";
				}
				function knight2() {
					document.getElementById('knight').style.background = "url(knight.png) no-repeat -22px -75px"
					document.getElementById('knight').style.width = "61px";
					document.getElementById('knight').style.height = "44px";
				}
			}
			knightAnimation();
			
			function nextQues() {
					choice = 0;
					wrong = false;
					newQues();
				}
				
			function homePage() {
				window.open("index.html", "_self");
			}
			newQues();
		</script>
	</body>
</html>
