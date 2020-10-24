<?php

function setup() {
	$ms = ["Zeus", "Apollo", "Hermes", "Ares", "Hades", "Poseidon", "Dionysus"];
	$fs = ["Demeter", "Aphrodite", "Artemis", "Hera", "Athena", "Hestia"];
	$characters = [];
	$template = ["name"=>"", "sex"=>"", "present"=>0, "sleeping"=>0, "mode"=>0];
	foreach($ms as $god) {
		$template["name"] = $god;
		$template["sex"] = "m";
		$template["mode"] = rand(0, 3);
		$characters[] = $template;
	}
	foreach($fs as $god) {
		$template["name"] = $god;
		$template["sex"] = "f";
		$template["mode"] = rand(0, 3);
		$characters[] = $template;
	}
	$GLOBALS["gods"] = $characters;
	$GLOBALS["text"] = "";
	$GLOBALS["lastpara"] = 0;
	$GLOBALS["hero"] = $GLOBALS["current"] = random(gods())["name"];
	$GLOBALS["object"] = "";
	$GLOBALS["scenes"] = [
["name"=>"lost", "cast_size"=>1, "story"=>"quest", "suite"=>["environment", "drink", "story", "posture", "fiddle", "frustration", "stir", "weather", "dream"]],
["name"=>"rain", "cast_size"=>2, "story"=>"rain", "suite"=>["stir", "dream", "music", "they", "interact", "posture", "express", "misgiving", "story", "mood"]],
["name"=>"birds", "cast_size"=>2, "story"=>"birds", "suite"=>["move", "hesitate", "eat", "drink", "interact", "express", "posture", "fiddle", "story"]],
["name"=>"temples", "cast_size"=>2, "story"=>"temples", "suite"=>["environment", "philosophy", "they", "mood", "frustration", "posture", "wistful", "story"]],
["name"=>"radio", "cast_size"=>3, "story"=>"radio", "suite"=>["thinkers", "they", "intent", "mood", "posture", "friends", "story", "depart"]]
	];
	$GLOBALS["finale"] = ["name"=>"found", "cast_size"=>1, "story"=>"find", "suite"=>["optimism", "alone", "story", "relax", "stir", "dream", "tidy"]];
	$GLOBALS["scene_count"] = 0;
	$GLOBALS["scene_params"] = [];
	$GLOBALS["scene_cast"] = [];
}

function gods($status="") {
	$gods = $GLOBALS["gods"];
	$return = [];
	foreach($gods as $god) {
		if($status=="") {
			$return[] = $god;
		} elseif($status=="awake" && $god["sleeping"]==0) {
			$return[] = $god;
		} elseif($status=="asleep" && $god["sleeping"]==1) {
			$return[] = $god;
		} elseif($status=="present" && $god["present"]==1) {
			$return[] = $god;
		} elseif($status=="absent" && $god["present"]==0) {
			$return[] = $god;
		} elseif($status=="present,awake" && $god["sleeping"]==0 && $god["present"]==1) {
			$return[] = $god;
		}
	}
	return $return;
}

function godget($name) {
	foreach($GLOBALS["gods"] as $gi=>$god) {
		if($name==$god["name"]) {
			return $GLOBALS["gods"][$gi];
		}
	}
}

function godset($name, $setting, $value) {
	foreach($GLOBALS["gods"] as $gi=>$god) {
		if($name==$god["name"]) {
			$GLOBALS["gods"][$gi][$setting] = $value;
		}
	}
	return true;
}

function godsreset() {
	foreach($GLOBALS["gods"] as $gi=>$god) {
		$GLOBALS["gods"][$gi]["present"] = 0;
		$GLOBALS["gods"][$gi]["sleeping"] = 0;
	}
	return true;
}

function godlist($opts="all") {
	$gl = [];
	foreach($GLOBALS["gods"] as $god) {
		if($god["name"] != $GLOBALS["hero"] && $opts=="nohero") {
			$gl[] = $god["name"];
		} elseif($opts=="all") {
			$gl[] = $god["name"];
		}
	}
	return $gl;
}

function sex($name) {
	$god = godget($name);
	return $god["sex"];
}

function awake($name) {
	if(godget($name)["sleeping"]==0) {
		return true;
	} else {
		return false;
	}
}

function present($name) {
	if(godget($name)["present"]==1) {
		return true;
	} else {
		return false;
	}
}

function curr($name="") {
	if($name=="") {
		return $GLOBALS["current"];
	} else {
		$GLOBALS["current"] = $name;
	}
}

function object() {
	$o = ["clock", "sideboard", "table", "armchair", "window", "blinds", "lamp", "hearth", "television", "radio", "wireless", "bookcase", "books", "desk", "flowers on the sideboard", "plants", "coffee pot", "wine boxes in the corner", "empty wine boxes", "refrigerator", "wooden stool", "clay pots"];
	return "the " . random($o);
}

function pronouns($god) {
	$sex = sex($god);
	$pronouns = ["she", "she", "herself", "hers", "her", "her"];
	if($sex=="m") {
		$pronouns = ["he", "he", "himself", "his", "him", "his"];
	}
	return $pronouns;
}

function pronounise($text, $name) {
	$templ = ["NAME", "SHE", "HERSELF", "HERS", "HIM", "HER"];
	$pr = pronouns($name);
	if(curr() != $name) {
		$pr[0] = $name;
	}
	for($i=0;$i<count($templ);$i++) {
		$text = str_replace($templ[$i], $pr[$i], $text);
	}
	return $text;
}

function mode($name) {
	return godget($name)["mode"];
}

function random($a, $n=1) {
	$na = array_rand($a, $n);
	if($n==1) {
		return $a[$na];
	} else {
		$ret = [];
		foreach($na as $ne) {
			$ret[] = $a[$na];
		}
		return $ret;
	}
}

function words() {
	return str_word_count($GLOBALS["text"]);
}

function scene_num() {
	$num = "";
	$n = $GLOBALS["scene_count"];
	$nums = ['l'=>50, 'xl'=>40, 'x'=>10, 'ix'=>9, 'v'=>5, 'iv'=>4, 'i'=>1];
	while($n > 0) {
		foreach($nums as $ni=>$nr) {
			if($n >= $nr) {
				$num .= $ni;
				$n -= $nr;
				break;
			}
		}
	}
	return $num;
}

function addtext($t) {
	$t = ucfirst($t);
	if($GLOBALS["lastsentence"] != $t) {
		$GLOBALS["text"] .= $t;
		$GLOBALS["lastsentence"] = $t;
		if(substr($t, -1) != "\n") {
			$GLOBALS["text"] .= " ";
		}
	}
}

function para() {
	$np = rand(50,150);
	$wc = words();
	if($wc - $GLOBALS["lastpara"] > $np) {
		addtext("\n    ");
		$GLOBALS["lastpara"] = $wc;
	}
}

function sentence() {
	$s = $GLOBALS["scene_params"]["suite"];
	$f = random($s);
	$f();
	para();
}

function scene() {
	godsreset();
	$GLOBALS["scene_params"] = array_shift($GLOBALS["scenes"]);
	if(count($GLOBALS["scenes"])==0 && isset($GLOBALS["finale"])) {
		$GLOBALS["scenes"][] = $GLOBALS["finale"];
		unset($GLOBALS["finale"]);
	} else {
		shuffle($GLOBALS["scenes"]);
	}
	$GLOBALS["scene_count"]++;
	$GLOBALS["scene_cast"] = [$GLOBALS["hero"]];
	$GLOBALS["current"] = "";
	$GLOBALS["lastpara"] = words();
	$gl = godlist("nohero");
	shuffle($gl);
	for($i=1;$i<$GLOBALS["scene_params"]["cast_size"];$i++) {
		$GLOBALS["scene_cast"][] = array_pop($gl);
	}
	foreach($GLOBALS["scene_cast"] as $god) {
		godset($god, "present", 1);
	}
	$st = $GLOBALS["scene_params"]["story"];
	if($st!="") {
		$st();
	} else {
		quest();
	}
	if(substr($GLOBALS["text"], -1) == " ") {
		addtext("\n\n\n\n");
	}
	$GLOBALS["text"] .= scene_num() . "\n\n";
	while(count($GLOBALS["story"])>0) {
		sentence();
	}
}
 
function printout() {
	setup();
	while(count($GLOBALS["scenes"])>0) {
		scene();
	}
	$t = $GLOBALS["text"];
	$t = str_replace("    ", "&nbsp;&nbsp;&nbsp;&nbsp;", $t);
	echo nl2br($t);
	echo "<p><i>(" . words() . " words)</i></p>";
}

function arrive() {
	$p = gods("present");
	if(count($p)<$GLOBALS["scene_params"]["cast_size"]) {
		$n = gods("absent");
		$ng = random($n);
		if(!isset($GLOBALS["hero"])) {
			$GLOBALS["hero"] = $ng;
		}
		$name = $ng["name"];
		godset($name, "present", 1);
		$a = ["arrived", "appeared in the doorway", "came in", "opened the door and came in", "entered", "returned", "was back", "turned up", "came back inside"];
		addtext(pronounise("NAME " . random($a) . ".", $name));
		curr($name);
	} else {
		depart();
	}
}

function depart() {
	$p = gods("present");
	if(count($p)>1) {
		$n = gods("present");
		$ng = random($n);
		$name = $ng["name"];
		if(godget($name)["sleeping"]==0) {
			godset($name, "present", 0);
			$l = ["left", "went to get more cigarettes", "went to buy wine", "went outside", "went out", "decided to go away for a while", "went away again", "decided to leave", "opened the door and slipped out", "went to get more supplies", "went in search of more beer", "decided to go outside", "got up and left", "went in search of something else, anything else", "put on HER hat and coat and went outside", "took HER coat and went out through the door"];
			addtext(pronounise("NAME " . random($l) . ".", $name));
			curr($name);
		} 
	} else {
		arrive();
	}
}

function stir() {
	$god = random(gods("present"));
	$name = $god["name"];
	if($god["sleeping"]==0) {
		if(rand(0,3)==0) {
			godset($name, "sleeping", 1);
			$t = ["NAME went to sleep", "NAME fell asleep", "NAME closed HER eyes and sank into sleep", "NAME closed HER eyes and slept", "NAME closed HER eyes, slept", "NAME soon fell into a deep sleep"];
			addtext(pronounise(random($t), $name) . ".");
			curr($name);
		}	
	} else {
		godset($name, "sleeping", 0);
		$t = ["NAME woke up", "NAME stirred", "NAME opened HER eyes", "NAME stirred and rubbed HER eyes", "NAME got up again", "NAME stirred and stood up", "NAME woke suddenly"];
		addtext(pronounise(random($t), $name) . ".");
		curr($name);
	}
}

function dream() {
	$s = gods("asleep");
	if(count($s)>0) {
		$god = random($s);
		$name = $god["name"];
		$de = ["brooding dragons", "treasure", "insects", "darkness", "indistinct forms", "eyes in walls", "infamy", "houses filled with earth", "fissures", "formless shapes", "raisin cake", "abandonment", "labyrinths", "castle towers", "deep, deep lakes", "high structures", "remote islands", "lemon groves", "shining seas", "regret", "quicksilver"];
		$d2 = $d3 = "";
		for($i=0;$i<2;$i++) {
			$dn = rand(0, count($de)-1);
			$d2 .= $de[$dn] . " and ";
			array_splice($de, $dn, 1);
		}
		$d2 = substr($d2, 0, strlen($d2)-5);
		$d3 = random($de) . ", " . $d2;
		$d = ["distant lands", "long summer days", "ancient mistakes", "empires buried in sand", $d2, $d3, "warm days and simpler times", "mountains covered with thick snow", "a wide plain with a lake of glass", "streets with empty doorways", "a fortress with high walls", "a high plain", "high plains", "a deep, gleaming lake", "the labyrinth", "an endless series of corridors and rooms"];
		addtext(pronounise("NAME dreamed of " . random($d) . ".", $name));
		curr($name);
	}

}

function move() {
	$g = gods("present,awake");
	if(count($g)>0) {
		$name = random($g)["name"];
		$o = random(["bookcase", "window", "table", "armchair"]);
		$d = random(["telephone", "radio", "television", "lamp"]);
		$r = random(["clay pots", "wine boxes", "drawers", "cupboards in the kitchenette"]);
		$q = random(["a packet of cigarettes", "coins", "discarded currency", "liquor"]);
		$a = ["paced in circles", "walked backwards and forwards over the floorboards", "tried balancing on one foot", "sat quietly", "stretched", "did some handstands", "looked around for $q", "smoked a cigarette", "fancied a drink", "began to make some coffee", "thought about somewhere far away", "tried to work the $d", "sat down", "stood up", "searched the $r for $q", "began looking through the $r for $q", "was looking through all the $r", "was looking for $q", "drank a glass of wine", "downed a cup of coffee", "began to feel a fragility in HER legs", "went over to the $o", "leaned HER head against the $o"];
		addtext(pronounise("NAME " . random($a) . ".", $name));
		curr($name);
	}
}

function hesitate() {
	$g = gods("present,awake");
	if(count($g)>0) {
		$name = random($g)["name"];
		$h = ["glanced at", "looked at", "placed HER hand on", "ran HER fingers over", "considered", "looked intently at", "stared at", "was gazing at", "crossed over to", "moved over to", "went to", "walked over to", "stepped over to"];
		addtext(pronounise("NAME " . random($h) . " " . object() . ".", $name));
		curr($name);
	}
}

function eat() {
	$g = gods("present,awake");
	if(count($g)>0) {
		$name = random($g)["name"];
		$f = ["an orange", "some cake", "a slice of toast", "some biscuits", "a bowl of oats", "a piece of chocolate", "the rest of the fish and chips", "some cheese and slices of apple", "a thin slice of chicken", "one of those bitter little fruits", "one of the apples", "a few raspberries"];
		$a = ["ate", "consumed", "considered eating", "ate", "ate", "chewed on", "began eating", "wanted to eat", "thought about eating", "began to consume", "had a sudden craving for", "wanted", "craved", "hungered for"];
		addtext(pronounise("NAME " . random($a) . " " . random($f) . ".", $name));
		curr($name);
	}
}

function drink() {
	$g = gods("present,awake");
	if(count($g)>0) {
		$name = random($g)["name"];
		$f = ["a cup of wine", "a glass of wine", "another glass of wine", "a glass of beer", "another beer", "a cup of coffee", "a glass of water", "a cup of water", "a cup of milk", "some milk", "more water"];
		$a = ["tasted", "carefully sipped", "wanted", "had the urge to drink", "needed", "was in the mood for", "thought of drinking", "drank", "downed", "drank", "sipped", "slurped", "suppressed the desire for", "decided on", "decided against", "yearned for", "thirsted for", "was thirsty for"];
		addtext(pronounise("NAME " . random($a) . " " . random($f) . ".", $name));
		curr($name);
	}
}

function interact() {
	$g = gods("present,awake");
	if(count($g)>1) {
		shuffle($g);
		$g1 = array_pop($g);
		$name = $g1["name"];
		$g2 = array_pop($g);
		$i = ["looked at", "frowned at", "stared at", "looked over towards", "glanced at", "glanced over at", "smiled at", "nodded towards"];
		addtext(pronounise("NAME " . random($i) . " " . $g2["name"] . ".", $name));
		curr($name);
	}
}

function express() {
	$g = gods("present,awake");
	if(count($g)>1) {
		$name = random($g)["name"];
		$i = ["smiled", "grimaced", "felt confused", "felt strange", "felt tense", "looked up", "looked away", "sighed", "grinned", "laughed", "groaned", "gulped", "wasn't looking forward to this", "seemed tense", "seemed more relaxed", "felt tired", "felt sick", "felt good", "frowned", "looked confused", "didn't look well", "didn't look quite HER normal self"];
		addtext(pronounise("NAME " . random($i) . ".", $name));
		curr($name);
	}
}

function weather() {
	$i = ["The wind was howling", "Rain was battering the roof", "There were dark clouds on the horizon", "Darkness covered the sky", "There was a storm coming", "The sky had patches of light and dark", "The rain had stopped", "Nobody seemed to know how long this weather would last", "Rain was hammering on the window", "The window was filled with light", "Outside, the winds were gathering strength"];
	addtext(random($i) . ".");
}

function environment() {
	$s = random(["deep underground", "far away", "nearby", "upstairs", "in the vicinity"]);
	$i = ["Time passed", "There was only the sound of the clocks ticking", "Somewhere $s, a bell began to ring", "The air seemed heavy", "Shadows moved across the floor", "Shadows passed over the floor", "Somewhere far off, a trumpet sounded", "Somewhere $s, the pipes were rattling", "The floorboards were creaking", "Somewhere $s, somebody was blowing a whistle", "Somewhere $s, there was the sound of shattering glass", "There was the sound of static", "There were the odours of coffee brewing", "There were the sounds of food being prepared"];
	addtext(random($i) . ".");
}

function music() {
	$g = gods("present,awake");
	$m = random(["music", "a song", "singing", "music playing", "chanting", "a choir"]);
	if(count($g)>1) {
		$name = random($g)["name"];
		$i = ["NAME thought SHE could hear $m", "There was the distant sound of $m", "NAME opened the door and listened to the distant singing", "NAME listened. The strains of $m were unmistakeable but distant and indistinct", "NAME thought the sounds coming from the water pipes sounded like $m", "The vibrations of the floorboards were like $m, NAME thought"];
		addtext(pronounise(random($i) . ".", $name));
		curr($name);
	}
}

function philosophy() {
	$g = gods("present,awake");
	if(count($g)>1) {
		$name = random($g)["name"];
		$p = random(["stoics", "philosophers", "nihilists", "sceptics", "materialists", "rationalists", "idealists", "pragmatists", "existentialists"]);
		$i = ["So it goes", "This sort of thing happens all the time", "Everyone is alone", "Some people never learn", "This makes no sense", "I don't want to know", "I must be dreaming", "I feel like I'm going crazy", "Every day is the same", "Maybe the $p were right all along", "I don't like this", "You never cross the same stream twice", "There must be some alternative to this", "This can't go on", "I think everything is going to be okay", "This will soon be over", "This doesn't sound promising", "The portents are bad", "I don't like the look of the prophecies"];
		$s = "said NAME";
		if(curr()==$name) { $s = "SHE said"; }
		addtext(pronounise(random($i) . ", " . $s . ".", $name));
		curr($name);
	}
}

function thinkers() {
	$g = gods("present,awake");
	if(count($g)>1) {
		$name = random($g)["name"];
		$p = random(["Aristotle", "Plato", "Zeno", "Pythagoras", "Socrates", "Democritus", "Epicurus", "Diogenes", "Philo"]);
		$s = "said NAME";
		if(curr()==$name) { $s = "SHE said"; }
		$i = ["This is exactly what $p said would happen, $s.", "NAME wondered what $p would make of all this.", "NAME wasn't sure what to make of all this.", "$p was just a man, $s, you have to remember that.", "I was just thinking about $p, $s.", "$p, $s, was always going on about this sort of thing.", "Things change, $s, and even $p is gone.", "NAME noticed one of the books on the shelf was by $p.", "NAME took one of the books from the shelf, a selection of texts by $p.", "From now on, $s, I'm only going read $p."];
		addtext(pronounise(random($i), $name));
		curr($name);
	}
}

function intent() {
	$g = gods("present,awake");
	$o = random(["halls of stone", "temple precincts", "an old shepherd's hut", "woodland groves"]);
	$m = random(["deep lakes", "high plains", "citadels", "stone towers scraping the sky", "glass towers", "high castle walls", "great doorways"]);
	if(count($g)>1) {
		$name = random($g)["name"];
		$i = ["thought about going outside", "wanted to go back to those days, long ago", "thought about other days, other times", "thought about other faces, other rooms", "was thinking about $o", "wanted to be somewhere with $o and $m", "became aware of the sudden absence of $m and $o", "smiled, remembering $m, $o"];
		addtext(pronounise("NAME " . random($i) . ".", $name));
		curr($name);
	}	
}

function friends() {
	$g = gods("present,awake");
	$f = random(["Galatea", "the Minotaur", "Theseus", "Andromeda", "the Medusa", "Helen", "Circe", "Asterion", "the Centaur", "Helios"]);
	$a = random(["danced on", "lay under", "stood on", "jumped onto"]);
	$l = random(["a table", "the temple dais", "a mountain summit", "an armchair"]); 
	$p = random(["party", "time", "dinner party", "feast", "celebration", "event", "festival"]);
	if(count($g)>1) {
		$name = random($g)["name"];
		$s = "said NAME";
		if(curr()==$name) { $s = "NAME said"; }
		$i = ["I remember $f, $s, do you?", "I wonder whatever happened to $f? $s.", "The days of $f and all the nymphs, those were good days, $s.", "I remember that $p with $f, $s.", "NAME thought of the times when $f was still around.", "NAME was thinking about $f and how brief those days turned out to be.", "I remember that $p , $s, when $f $a $l and made us laugh.", "Remember that $p, $s, when $f $a $l?", "I remember $f $a $l, $s."];
		addtext(pronounise(random($i), $name));
		curr($name);
	}
}

function wistful() {
	$g = gods("present,awake");
	if(count($g)>1) {
		$name = random($g)["name"];
		$s = "said NAME";
		if(curr()==$name) { $s = "NAME said"; }
		$i = ["People used to love me, $s, in those days.", "I remember the tributes, $s. Don't you?", "NAME thought those temples would last forever.", "The candles were guttering in the draughts coming under the doors. It's cold, $s.", "We have a lot to be thankful for, $s.", "NAME picked up one of the little figurines on the mantelpiece.", "NAME picked up one of the figurines and looked at it."];
		addtext(pronounise(random($i), $name));
		curr($name);
	}
}

function they() {
	$g = gods("present,awake");
	if(count($g)>1) {
		$i = ["were silent", "looked at each other", "considered the situation", "reflected on things", "tried to think of something to say", "were lost in their own thoughts", "remained silent", "laughed", "listened to the creaking floorboards", "listened to the sound of the wind"];
		addtext("They " . random($i) . ".");
		curr("none");
	}
}

function mood() {
	$name = curr();
	if(awake($name) && present($name)) {
		$s = ["anger", "annoyance", "confusion", "dislocation", "wakefulness", "determination"];
		$m = ["scratched HER nose", "folded HER arms", "looked away", "felt nauseous", "checked HER appearance in the mirror", "had a sudden memory of youth", "adjusted HER shoes", "changed HER coat", "checked HERSELF in the mirror", "tied on a woollen scarf", "wasn't sure", "looked out of the window", "had a sudden sense of " . random($s), "was overcome by a feeling of " . random($s), "wondered if SHE was losing HER touch", "touched HER hand to HER face", "looked at HER trembling hands", "looked at HER palms", "looked at HER hands"];
		addtext(pronounise("NAME " . random($m) . ".", $name));
		curr($name);
	}
}

function frustration() {
	$name = curr();
	if(awake($name) && present($name)) {
		$f = random(["lost", "dislocated", "afraid", "encouraged", "unsure"]);
		$c = random(["older", "younger", "more pale", "uncertain", "hesitant"]);
		$m = ["tried to read the newspaper but the words were blurred and indistinct", "walked to the window and pressed HER nose against the glass", "wanted to say something but wasn't sure what", "wanted to say something", "felt $f, in some vague sense", "seemed $f", "knew something wasn't quite right", "had the sense of being $f", "had a sinking feeling about the whole thing", "didn't want this. It didn't seem worth all HER sacrifices", "was losing HER edge, maybe", "was losing perspective", "needed to be more objective", "wanted better than this, wanted more", "looked $c somehow", "looked a little $c", "looked pale and HER eyes were glassy"];
		addtext(pronounise("NAME " . random($m) . ".", $name));
		curr($name);
	}
}

function misgiving() {
	$name = curr();
	if(awake($name) && present($name)) {
		$m = ["had no memory of anything", "hesitated", "exhaled and said nothing", "stared at the floor and said nothing", "swallowed, said nothing", "looked around as if remembering where SHE was", "was quiet", "was silent", "exhaled", "sniffed", "inhaled abruptly", "had a strange expression", "frowned", "looked at the back of HER hands", "crossed HER arms and sighed"];
		addtext(pronounise("NAME " . random($m) . ".", $name));
		curr($name);
	}
}

function posture() {
	$name = curr();
	if(awake($name) && present($name)) {
		$m = ["Looking at HER hands, SHE murmured quietly", "SHE folded HER arms", "HER limbs felt tired and sore", "HER limbs were heavy", "SHE felt the energy draining from HER body", "SHE stretched HER arms", "SHE gently pressed HER hands together", "SHE closed HER eyes and murmured quietly", "The sounds around HIM seemed muffled and indistinct, like SHE was underwater", "SHE rubbed the tendons in HER arms", "SHE massaged HER wrists", "SHE rubbed HER wrists", "SHE turned HER head slowly from side to side"];
		addtext(pronounise(random($m) . ".", $name));
		curr($name);
	}
}

function relax() {
	$name = curr();
	if(awake($name) && present($name)) {
		$m = ["Looking at HER hands, SHE smiled to HERSELF", "SHE folded HER arms", "HER limbs felt lithe and powerful", "HER limbs were lighter", "SHE felt HER body filling with light", "SHE stretched HER arms", "SHE gently pressed HER hands together", "SHE closed HER eyes and breathed deeply", "The sounds around HIM seemed bright and melodious, like SHE was floating on air", "SHE rubbed the tendons in HER arms", "SHE massaged HER wrists", "SHE rubbed HER wrists", "SHE turned HER head slowly from side to side"];
		addtext(pronounise(random($m) . ".", $name));
		curr($name);
	}
}

function fiddle() {
	$name = curr();
	if(awake($name) && present($name)) {
		$m = ["SHE drew back the curtains", "Pressing the buttons on the radio, SHE began to dial through the static", "SHE flipped the switches on the television, staring into the blank, dead screen", "SHE opened the door, closed it again", "SHE looked through the books on the shelf", "SHE picked up the newspaper and paged through it", "SHE rearranged the empty wine boxes next to the fireplace", "SHE pressed the switches on the radio and held HER ear against the speaker", "SHE pressed the buttons on the television set", "SHE picked up a book and looked through the pages", "SHE picked up a book", "SHE browsed through the newspaper", "SHE took one of the books from the shelf", "SHE stoked the fire", "SHE scooped more coal onto the fire", "SHE crouched at the hearth and looked into the flames", "SHE crouched next to the hearth"];
		addtext(pronounise(random($m) . ".", $name));
		curr($name);
	}
}

function alone() {
	$name = curr();
	if(awake($name) && present($name)) {
		$fb = random(["wine", "beer", "cigarettes", "liquor", "food", "supplies", "consumables", "fish and chips"]);
		$o = random(["television", "windows", "mantelpiece", "bookcase", "window frames", "chairs", "table", "lamps", "mirror"]);
		$m = ["NAME sighed. They had run out of $fb again.", "The others had all gone in search of more $fb.", "NAME should have liked more $fb, if there were any left.", "NAME tidied all the books on the bookshelf.", "NAME cleared out the fire and straightened the furniture.", "NAME dusted down the radio, and pushed the television back into the corner.", "NAME took the cloth and wiped down the $o."];
		addtext(pronounise(random($m), $name));
		curr($name);
	}
}

function tidy() {
	$g = gods("present,awake");
	if(count($g)>1) {
		$name = $g[0];
		$i = ["NAME opened the window and brushed the floorboards.", "NAME took out the empty wine boxes and cleared the table. SHE cleaned out the coffee pot and wiped down the stove.", "NAME straightened the picture frames.", "NAME sat down and read the weather forecast in the newspaper, looked at the puzzles.", "NAME looked at the figurines on the mantelpiece.", "NAME picked up one of the figurines from the mantelpiece."];
		addtext(pronounise(random($i), $name));
		curr($name);
	}
}

function optimism() {
	$s = random(["light", "blue", "warm", "serene", "calm", "quiet", "luminous"]);
	$o = random(["still", "gentle", "muted"]);
	$r = random(["mirror", "window", "lamp glass"]);
	$m = ["The sky was $s.", "The skies were $s, and the waves on the sea more $o.", "The curtains lifted in the breeze.", "The air was fresher, cleaner.", "Sunlight was reflecting in the $r.", "The $r reflected the sun."];
	addtext(random($m));
}

function story() {
	if(count($GLOBALS["story"]) > 0) {
		$name = curr();
		if(awake($name) && present($name)) {
			$s = 
		addtext(pronounise(array_shift($GLOBALS["story"]), $name));
		}
	}
}

function quest() {
	$o = random(["bronze sword", "gilded spear", "crystal goblet", "porcelain flask", "red violin", "seven-stringed lyre", "remote control", "magnifying glass"]);
	$GLOBALS["object"] = $o;
	$GLOBALS["story"] = ["NAME opened all the drawers, closed them again.", "SHE searched the cupboards and the clay pots.", "NAME remembered the $o.", "Where was the $o?", "A short time later, NAME thought about the $o.", "NAME dragged a chair over to the bookcase, climbed up and looked on top. No $o.", "NAME searched the cupboards, and under all the chairs, opened all the drawers and closed them again.", "NAME went through all the empty wine boxes.", "That $o will never be found, SHE thought."];
}

function rain() {
	$GLOBALS["story"] = ["The rain seemed to be more intense.", "It was still raining.", "Rain hammered on the window.", "The sound of the rain on the roof seemed louder.", "When was this rain going to stop?", "There were reports of floods on the evening news bulletins.", "Somewhere out there, rivers were breaking their banks.", "All of the streets, in all of the towns now were flooded, impassable.", "The rain was never going to stop."];
}

function birds() {
	$b = random(["buzzard", "crow", "starling", "vulture", "jackdaw", "herring gull", "sea eagle", "petrel", "grey albatross"]);
	$GLOBALS["story"] = ["NAME looked out of the window, watching the lazy flight of a $b crossing the sky.", "Another bird flew overhead, heading towards the west.", "NAME stood by the window. More birds were passing between the clouds.", "The calls of the birds were getting louder.", "The sky was deep red.", "The sky seemed to be filled with birds.", "There was the land and the sea, murky under the red clouds.", "The sky was clear. The birds seemed to have gone.", "The pale face of the moon illuminated the sky."];
}

function radio() {
	$GLOBALS["story"] = ["NAME crouched next to the radio, adjusting its switches and dials.", "The radio, NAME said, is it working yet?", "NAME tried again to get the radio to work, adjusting the tuner with HER ear to the speaker.", "The radio is defunct, SHE said. It's never going to work.", "A sudden burst of static interrupted their thoughts, followed by a series of modulations. The radio had come back to life.", "The urgent tones of a news bulletin sounded from the radio set.", "Someone turn the volume down, SHE said.", "The stream of news bulletins from the radio had become an endless cascade of gloom.", "I wish somebody would turn off that damned radio, SHE said."];
}

function temples() {
	$GLOBALS["story"] = ["NAME looked at the picture hanging over the fireplace.", "I remember the colonnades my first temple, NAME said", "NAME made HERSELF comfortable in the armchair. Those temples were full of gold, SHE said.", "My temples were always filled with priests, NAME said. Do you remember?", "NAME went to the bookcase and ran HER fingers over the spines of the books.", "NAME took a book down from the shelf. Perhaps the temples are bigger in our memory, NAME said, and maybe we forget.", "It all seemed a long time ago, and far away, all those lemon trees and olive groves.",  "NAME was thinking about temples, filled with statues, tapestries and the glow of candles."];
}

function find() {
	$o = $GLOBALS["object"];
	$s = random(["calm", "serenity", "transcendence", "contentment"]);
	$w = random(["far away", "deep underground", "high and clear"]);
	$p = random(["bookcase", "mantelpiece", "table", "book shelf", "window sill"]);
	$GLOBALS["story"] = ["The mirror was catching the light from the window.", "The pipes of the heating system were quiet.", "The radio was silent.", "NAME lay down on the floor of the kitchenette and breathed deeply, feeling a sense of $s. Turning HER head, SHE laid HER cheek against the floorboards, noticing under the sink unit, surrounded by empty wine bottles, the distinctive form of a $o. Sighing, SHE took it up and set it on the $p.", "Somewhere $w, a bell began to ring."];
}

?>
<!DOCTYPE html>
<html>
	<head>
		<title>immortals</title>
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />   
		<meta charset="utf-8" />  
		<link href="https://fonts.googleapis.com/css?family=Libre+Baskerville:400,400i,700" rel="stylesheet" />
		<style type="text/css">
			body { background: #fff; color: #444; font-family:  'Libre Baskerville',serif;  font-size: 8pt; font-variant-ligatures: common-ligatures; text-align: center; font-size: 16px;}
			h1 { color: #666; border-bottom: 1px solid #ccc; }
			hr { height: 0px; border: 0px; border-bottom: 1px solid #ccc; }
			div { margin: 0 auto; text-align: left; width: 90%; max-width: 600px; }
			.footnote { font-size: 12px; }
		</style>
	</head>
	<body>
		<div>
			<br />
			<h1>The Immortals</h1>
			<p><i>A computer-generated text for NaNoWriMo 2020. <b>Refresh the page for a new incarnation.</b></i></p>
			<?php printout(); ?>
			<hr />
			<p class="footnote">Version ii, 2020</p>
		</div>
	</body>
</html>
