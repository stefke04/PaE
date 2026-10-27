# Lecture 5 (PaE): Utilitarianism, Mill, Singer. Full tutoring session

This file contains the complete tutoring session on lecture 5: every teaching point (text, boxed takeaway), every visual as full HTML/SVG source, every quiz as full HTML/JavaScript source, and the side questions with their answers. It is self-contained: you do not need the original artifacts.

Sources used in the repo (`stefke04/PaE`): `Lecture 5.txt` (transcript), `4. Utilitarianism.pdf` (scanned slides, no text layer), `4. Singer_The Life You Can Save ... excerpt.pdf`. The session was taught mainly from the transcript.

## How to use the code

* Every **visual** is one complete HTML file. Save the code block as `pN_visual.html` and open it in a browser (dark panel, inline SVG).
* Every **quiz** uses the same HTML/JS shell (given once in the section "Quiz shell"). Only the `const Q=[...]` array differs per point. To rebuild a quiz: paste the shell into `pN_quiz.html` and replace the placeholder line `/*QUESTIONS*/` with that point's `const Q=[...];` block.
* Quiz behaviour: answer options are shuffled for each question, one click per question, a wrong pick turns red with a cross, the correct option turns green with a check, and a reason line appears below.

---

## Quiz shell (shared by all 18 quizzes)

Replace `/*QUESTIONS*/` with the `const Q=[...];` block of the point you want.

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>
:root{--bg:#fff;--fg:#1a1a1a;--surf:#f1f1f1;--bd:#ccc}
@media (prefers-color-scheme:dark){:root{--bg:#111;--fg:#eee;--surf:#222;--bd:#444}}
body{margin:0;padding:16px;background:var(--bg);color:var(--fg);font-family:system-ui,sans-serif}
.q{margin-bottom:22px}.p{font-weight:600;margin-bottom:8px}
button{display:block;width:100%;text-align:left;margin:6px 0;padding:10px 12px;border-radius:8px;border:1px solid var(--bd);background:var(--surf);color:var(--fg);font-size:15px;cursor:pointer}
.r{margin-top:6px;font-size:14px}
</style></head><body><div id="root"></div>
<script>
/*QUESTIONS*/
const root=document.getElementById('root');
function sh(a){a=a.map((t,i)=>({t,i}));for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}return a}
Q.forEach((q,qi)=>{
 const d=document.createElement('div');d.className='q';
 d.innerHTML='<div class="p">'+(qi+1)+'. '+q.p+'</div>';
 const btns=[];let done=false;
 const rd=document.createElement('div');rd.className='r';
 sh(q.o).forEach(o=>{
  const b=document.createElement('button');b.textContent=o.t;b.dataset.i=o.i;btns.push(b);
  b.onclick=()=>{
   if(done)return;done=true;
   const ok=o.i===q.c;
   const paint=(el,col,pre)=>{el.style.setProperty('background',col,'important');el.style.setProperty('color','#fff','important');el.style.setProperty('border-color',col,'important');el.textContent=pre+el.textContent};
   const right=btns.find(x=>+x.dataset.i===q.c);
   if(ok){paint(b,'#1f7a3d','✓ ');rd.textContent=q.r}
   else{paint(b,'#b3261e','✗ ');paint(right,'#1f7a3d','✓ ');rd.textContent='Correct: '+q.o[q.c]+'. '+q.r}
  };
  d.appendChild(b);
 });
 d.appendChild(rd);root.appendChild(d);
});
</script></body></html>
```

---

## Orientation (before point 1)

Lecture 5 asks one basic question: can we decide what is right simply by looking at what our actions lead to, and counting how much good and harm they cause for everyone affected? The two thinkers we start with, Bentham and Mill, say yes. They also built a way of doing the counting, and then ran into trouble when they tried to apply it.

We go through it in two stages. First we build the theory with Bentham and Mill: what gets counted, how the counting works, and where it breaks down. Then we use it on a hard real-world case with Peter Singer: if everyone's wellbeing counts equally, does it matter that people who are suffering live far away from us?

(The slides in the repo are scanned images without text, so the teaching is based mainly on the lecture transcript.)

---

## Point 1. What do we look at to decide whether an action is right?

Most moral thinking asks what kind of act something is, for example whether it breaks a rule or a promise. Consequentialism asks something else: what does the act lead to? The reason is a basic fact about human beings. All of us are governed by pain and pleasure, nobody can escape that, so any good moral theory has to be built on it. The consequences that matter are therefore the pain and pleasure that follow from the act.

**Visual** (`p1_visual.html`): Action, then Consequences, then Pleasure (green) and Pain (red) for everyone affected.

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 300" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect x="0" y="0" width="760" height="300" fill="#111"/>
<rect x="20" y="105" width="150" height="80" rx="10" fill="#222" stroke="#888"/>
<text x="95" y="140" text-anchor="middle" fill="#eee" font-size="16" font-weight="600">Action</text>
<text x="95" y="162" text-anchor="middle" fill="#bbb" font-size="13">what you decide to do</text>
<line x1="170" y1="145" x2="250" y2="145" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<rect x="255" y="105" width="170" height="80" rx="10" fill="#222" stroke="#888"/>
<text x="340" y="140" text-anchor="middle" fill="#eee" font-size="16" font-weight="600">Consequences</text>
<text x="340" y="162" text-anchor="middle" fill="#bbb" font-size="13">what it leads to</text>
<line x1="425" y1="130" x2="500" y2="75" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<line x1="425" y1="160" x2="500" y2="215" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<rect x="505" y="40" width="235" height="70" rx="10" fill="#1f7a3d"/>
<text x="622" y="72" text-anchor="middle" fill="#fff" font-size="16" font-weight="600">Pleasure</text>
<text x="622" y="94" text-anchor="middle" fill="#fff" font-size="13">for everyone affected</text>
<rect x="505" y="180" width="235" height="70" rx="10" fill="#b3261e"/>
<text x="622" y="212" text-anchor="middle" fill="#fff" font-size="16" font-weight="600">Pain</text>
<text x="622" y="234" text-anchor="middle" fill="#fff" font-size="13">for everyone affected</text>
<text x="95" y="215" text-anchor="middle" fill="#888" font-size="12">not judged here</text>
<text x="622" y="280" text-anchor="middle" fill="#eee" font-size="13">the verdict is read off here</text>
</svg></body></html>
```

Look at the right-hand side of the diagram. The action itself is not judged. We follow it forward to its consequences and look at the pleasure and pain they bring to everyone affected. The theory also applies beyond humans, to any being that can feel pain and pleasure.

> **Takeaway:** an action is right or wrong because of the pleasure and pain it leads to, not because of what kind of act it is.

**Quiz** (`p1_quiz.html`):

```javascript
const Q=[
{p:"A friend asks you to keep a secret, and keeping it leads to a lot of harm for others. How does a consequentialist judge keeping it?",
 o:["By whether keeping a promise is a good kind of act in itself","By the pleasure and pain that keeping it leads to for everyone affected","By how you feel about your friend"],c:1,
 r:"The verdict comes from the consequences, not from the type of act."},
{p:"Why does the theory take pain and pleasure as its starting point?",
 o:["Because every being that can feel is governed by them, so a moral theory has to take them into account","Because pain and pleasure are rules made by society","Because only humans can feel them"],c:0,
 r:"It is a basic fact nobody escapes. And it is not only humans: any being that can feel pain and pleasure counts."},
{p:"Which of these is NOT something a consequentialist looks at?",
 o:["What the action leads to","Pleasure and pain of those affected","Whether the act is of a forbidden kind, regardless of what it leads to"],c:2,
 r:"The kind of act, apart from its results, plays no role in this theory."}
];
```

### Your question after point 1

> *Does this state the consequence is either pleasure or pain for all people, because I would argue that an action could create pleasure for some people and pain for others.*

No, the theory does not say that, and the diagram was ambiguous on this. An action usually produces both, spread over different people. The theory weighs the two against each other: it determines the good and the bad results of each option and looks at the balance, the pleasures minus the pains, summed over everyone affected. That is why the lecture speaks of the greatest good for the greatest number. It also explains the refugee shelter example: about 100 to 200 refugees gain a lot (protection, a bed) and many schoolchildren lose a little (their sports hall). If the large gain outweighs the many small losses, the action is right.

Corrected takeaway for point 1: an action is right or wrong because of the balance of pleasure over pain it leads to, summed over everyone affected.

### Saved with `!!`

You marked this sentence for the summary: **"if the large gain outweighs the small losses, the action is right."** It was saved to `lecture5_notes.md` (see the end of this file) together with the refugee shelter example and the phrase "the greatest good for the greatest number" (Mill). A stop hook then asked to commit untracked files, so `lecture5_notes.md` was committed and pushed to branch `claude/clever-noether-ix1e7o`.

---

## Point 2. What do we do with the good: the rule to maximize

The first point told us what gets counted, pleasure and pain. The next question is what we are supposed to do with it. The answer is to promote the good by maximizing it, so that there is as much of it in the world as possible. This holds whatever you take the ultimate good to be, and the name of the good has changed over time. Bentham started with pleasure and pain, and his theory already spoke of happiness. Later it was called utility, welfare economists turned it into welfare, and today people usually say human wellbeing.

**Visual** (`p2_visual.html`): a row of names (pleasure and pain, happiness, utility, welfare, wellbeing) pointing to one green box "MAXIMIZE the good".

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 330" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="330" fill="#111"/>
<text x="380" y="28" text-anchor="middle" fill="#bbb" font-size="14">The name of "the good" changes over time ...</text>
<g font-size="15" font-weight="600" text-anchor="middle">
<rect x="15" y="50" width="150" height="64" rx="10" fill="#222" stroke="#888"/><text x="90" y="78" fill="#eee">Pleasure and pain</text><text x="90" y="98" fill="#bbb" font-size="12" font-weight="400">Bentham, original</text>
<rect x="195" y="50" width="130" height="64" rx="10" fill="#222" stroke="#888"/><text x="260" y="78" fill="#eee">Happiness</text><text x="260" y="98" fill="#bbb" font-size="12" font-weight="400">Bentham</text>
<rect x="355" y="50" width="130" height="64" rx="10" fill="#222" stroke="#888"/><text x="420" y="78" fill="#eee">Utility</text><text x="420" y="98" fill="#bbb" font-size="12" font-weight="400">later</text>
<rect x="515" y="50" width="115" height="64" rx="10" fill="#222" stroke="#888"/><text x="572" y="78" fill="#eee">Welfare</text><text x="572" y="98" fill="#bbb" font-size="12" font-weight="400">welfare economists</text>
<rect x="660" y="50" width="90" height="64" rx="10" fill="#222" stroke="#888"/><text x="705" y="78" fill="#eee">Wellbeing</text><text x="705" y="98" fill="#bbb" font-size="12" font-weight="400">today</text>
</g>
<g stroke="#aaa" stroke-width="2" marker-end="url(#a)"><line x1="165" y1="82" x2="193" y2="82"/><line x1="325" y1="82" x2="353" y2="82"/><line x1="485" y1="82" x2="513" y2="82"/><line x1="630" y1="82" x2="658" y2="82"/></g>
<line x1="380" y1="125" x2="380" y2="170" stroke="#aaa" stroke-width="2" stroke-dasharray="5 4"/>
<text x="395" y="152" fill="#bbb" font-size="13">whichever name you pick, the rule stays the same</text>
<rect x="190" y="175" width="380" height="80" rx="12" fill="#1f7a3d"/>
<text x="380" y="208" text-anchor="middle" fill="#fff" font-size="18" font-weight="700">MAXIMIZE the good</text>
<text x="380" y="232" text-anchor="middle" fill="#fff" font-size="14">"the greatest good for the greatest number" (Mill)</text>
<text x="380" y="290" text-anchor="middle" fill="#bbb" font-size="13">more of it is better, summed over everyone</text>
</svg></body></html>
```

The top row shows that the name of the good changed, while the bottom box shows that the rule stayed the same. One precision from point 1 still applies. "The greatest good for the greatest number" does not mean you must always side with the larger group. It means maximizing the total, so a big gain for a few can outweigh a small loss for many.

> **Takeaway:** whatever the good is called (pleasure, happiness, utility, welfare, wellbeing), the rule is to maximize it, summed over everyone affected.

**Quiz** (`p2_quiz.html`):

```javascript
const Q=[
{p:"Which statement about the names pleasure, happiness, utility, welfare and wellbeing is correct?",
 o:["They are different names for the good that the theory says to maximize","They are five separate moral theories","They name five different rules for what to do with the good"],c:0,
 r:"The name of the good changed over time, but the rule (maximize it) stayed the same."},
{p:"A policy gives a big gain to 100 people and costs 10,000 people a tiny inconvenience. If the total gain is larger than the total loss, what does the theory say?",
 o:["Reject it, because the larger group must always win","Accept it, because the total good is maximized","Reject it, because anyone who loses is a reason to refuse"],c:1,
 r:"The rule is to maximize the total, not to side with the bigger group."},
{p:"What does the theory tell us to do with the good, whatever we take it to be?",
 o:["Distribute it equally","Promote it by maximizing it","Leave it alone and avoid harm"],c:1,
 r:"We ought to promote the good, and we do so by maximizing it."}
];
```

### Your question: intrinsically good versus instrumentally good

Something is intrinsically good when it is good in itself, for its own sake. Something is instrumentally good when it is good only because it leads to something else that is good. Money is instrumentally good, because it matters only for what it buys or allows. Happiness is the standard intrinsic good, because if you ask "why do you want to be happy?", there is nothing further to point to. In the lecture, when we weigh an action we identify the intrinsically good and bad things it leads to (pleasure and pain for Bentham), and everything else counts only through its effect on those. Bentham also treats pleasure over pain as the ultimate good, the basic principle that cannot be derived from anything else. The word "instrumentally" is not in the lecture. It is a tutor addition, the standard contrast term.

---

## Point 3. How the calculation works

To know what the theory tells us in a concrete case, we need a procedure. It is the same for any decision or policy, and it is what Bentham wanted: ethics that works as close to the scientific method as possible. List your options. For each option, identify the intrinsically good and the intrinsically bad things it leads to. Then compute the balance for that option, meaning the pleasures minus the pains, and choose the option with the best balance.

**Visual** (`p3_visual.html`): the refugee shelter decision with invented numbers (marked in the picture as illustration, not from the lecture).

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 360" xmlns="http://www.w3.org/2000/svg">
<rect width="760" height="360" fill="#111"/>
<text x="380" y="26" text-anchor="middle" fill="#eee" font-size="15" font-weight="600">Decision: use the school sports hall as a refugee shelter?</text>
<text x="380" y="46" text-anchor="middle" fill="#bbb" font-size="12">all numbers are my invented illustration, not from the lecture</text>
<!-- column A -->
<rect x="30" y="65" width="320" height="270" rx="12" fill="#222" stroke="#888"/>
<text x="190" y="92" text-anchor="middle" fill="#eee" font-size="16" font-weight="700">Option A: open the hall</text>
<text x="46" y="125" fill="#bbb" font-size="13">150 refugees: protection, a bed</text>
<text x="334" y="147" text-anchor="end" fill="#6fdc8c" font-size="16" font-weight="700">150 × (+10) = +1500</text>
<text x="46" y="190" fill="#bbb" font-size="13">300 children: lose their sports hall</text>
<text x="334" y="212" text-anchor="end" fill="#ff8a80" font-size="16" font-weight="700">300 × (−2) = −600</text>
<line x1="46" y1="235" x2="334" y2="235" stroke="#888"/>
<text x="46" y="270" fill="#eee" font-size="14">Balance</text>
<rect x="190" y="285" width="144" height="38" rx="8" fill="#1f7a3d"/>
<text x="262" y="310" text-anchor="middle" fill="#fff" font-size="18" font-weight="700">+900</text>
<!-- column B -->
<rect x="410" y="65" width="320" height="270" rx="12" fill="#222" stroke="#888"/>
<text x="570" y="92" text-anchor="middle" fill="#eee" font-size="16" font-weight="700">Option B: keep the hall for sports</text>
<text x="426" y="125" fill="#bbb" font-size="13">150 refugees: no shelter (baseline)</text>
<text x="714" y="147" text-anchor="end" fill="#eee" font-size="16" font-weight="700">150 × 0 = 0</text>
<text x="426" y="190" fill="#bbb" font-size="13">300 children: keep their hall</text>
<text x="714" y="212" text-anchor="end" fill="#eee" font-size="16" font-weight="700">300 × 0 = 0</text>
<line x1="426" y1="235" x2="714" y2="235" stroke="#888"/>
<text x="426" y="270" fill="#eee" font-size="14">Balance</text>
<rect x="570" y="285" width="144" height="38" rx="8" fill="#444"/>
<text x="642" y="310" text-anchor="middle" fill="#fff" font-size="18" font-weight="700">0</text>
</svg></body></html>
```

Look at the green box in option A. A small loss for many children (-600) is outweighed by a large gain for a few refugees (+1500), so the balance is +900 and option A wins. If the children's loss had been larger than the refugees' gain, the same procedure would have chosen option B. The lecture gives this example without numbers, and the invented figures only show how the weighing works.

> **Takeaway:** for each option, add up the intrinsic goods and subtract the intrinsic bads over everyone affected, then choose the option with the best balance.

**Quiz** (`p3_quiz.html`):

```javascript
const Q=[
{p:"In the refugee shelter example, what makes option A the right choice in the utilitarian calculation?",
 o:["More people are helped than inconvenienced","The total gain outweighs the total loss","Refugees have more rights than schoolchildren"],c:1,
 r:"The verdict comes from the balance of gains minus losses, not from counting heads."},
{p:"Which of these is a step in the consequentialist calculation?",
 o:["Ask which option follows the most widely accepted rule","List the options, find the good and bad results of each, and compare the balances","Pick the option the decision maker feels most sympathy for"],c:1,
 r:"Sympathy is a gut reaction, which Bentham rejected. The calculation is structured per option."},
{p:"What does \"balance\" mean for one option?",
 o:["The pleasures minus the pains it leads to","The average of everyone\'s feelings","The number of people who benefit"],c:0,
 r:"The balance is the good results minus the bad results of that option."}
];
```

---

## Point 4. One person or a whole society: hedonism and utilitarianism

The calculation from point 3 can be run at two scales. In the simplest scenario it is done for one person only, because you only care about your own pleasure and pain as a result of your decision. That one-person version is hedonism: the theory that what matters morally is a person's subjective experience of pleasure and pain. The word has nothing to do with a luxurious lifestyle, which is what it suggests in everyday speech. Utilitarianism is the same calculation extended to everyone affected.

**Visual** (`p4_visual.html`): left panel hedonism (one person, "my pleasure minus my pain"), right panel utilitarianism (persons 1 ... n, "total balance").

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 330" xmlns="http://www.w3.org/2000/svg">
<rect width="760" height="330" fill="#111"/>
<rect x="20" y="20" width="320" height="290" rx="12" fill="#222" stroke="#888"/>
<text x="180" y="50" text-anchor="middle" fill="#eee" font-size="17" font-weight="700">Hedonism</text>
<text x="180" y="70" text-anchor="middle" fill="#bbb" font-size="13">the calculation for ONE person</text>
<circle cx="180" cy="130" r="26" fill="#3a6ea5"/>
<text x="180" y="136" text-anchor="middle" fill="#fff" font-size="14" font-weight="700">me</text>
<text x="180" y="190" text-anchor="middle" fill="#eee" font-size="14">my pleasure − my pain</text>
<rect x="95" y="215" width="170" height="40" rx="8" fill="#1f7a3d"/>
<text x="180" y="241" text-anchor="middle" fill="#fff" font-size="15" font-weight="700">my balance</text>
<text x="180" y="285" text-anchor="middle" fill="#bbb" font-size="12">easy: one person, one scale</text>
<rect x="420" y="20" width="320" height="290" rx="12" fill="#222" stroke="#888"/>
<text x="580" y="50" text-anchor="middle" fill="#eee" font-size="17" font-weight="700">Utilitarianism</text>
<text x="580" y="70" text-anchor="middle" fill="#bbb" font-size="13">the calculation for EVERYONE affected</text>
<g fill="#3a6ea5"><circle cx="470" cy="125" r="18"/><circle cx="520" cy="125" r="18"/><circle cx="570" cy="125" r="18"/><circle cx="620" cy="125" r="18"/><circle cx="670" cy="125" r="18"/></g>
<g fill="#fff" font-size="12" font-weight="700" text-anchor="middle"><text x="470" y="129">1</text><text x="520" y="129">2</text><text x="570" y="129">3</text><text x="620" y="129">…</text><text x="670" y="129">n</text></g>
<text x="580" y="190" text-anchor="middle" fill="#eee" font-size="14">add up everyone's pleasure − pain</text>
<rect x="495" y="215" width="170" height="40" rx="8" fill="#1f7a3d"/>
<text x="580" y="241" text-anchor="middle" fill="#fff" font-size="15" font-weight="700">total balance</text>
<text x="580" y="285" text-anchor="middle" fill="#ff8a80" font-size="12">hard: whose scale? how to compare?</text>
</svg></body></html>
```

Look at the red note under the right panel. Most of the criticism of utilitarianism comes from the difficulties of running the calculation at the scale of a society, or even globally. We meet several of them later: which pleasures count, how to measure them, and how to compare different people.

> **Takeaway:** hedonism is the one-person version of the calculation (my pleasure minus my pain), and utilitarianism extends it to everyone affected, which is where the difficulties start.

**Quiz** (`p4_quiz.html`):

```javascript
const Q=[
{p:"Sam only cares about his own pleasure and pain when deciding what to do. Which theory is he applying?",
 o:["Utilitarianism, because he counts pleasure and pain","Hedonism, the one-person version of the calculation","Asceticism"],c:1,
 r:"With one person, the calculation is hedonism. Utilitarianism counts everyone affected."},
{p:"In ethics, what does hedonism refer to?",
 o:["A luxurious lifestyle full of indulgence","The theory that what matters morally is a person\'s experience of pleasure and pain","The theory that suffering earns a reward in the afterlife"],c:1,
 r:"It is a moral theory, not a lifestyle. The suffering-for-reward view is asceticism, which comes later."},
{p:"Where does most of the criticism of utilitarianism come from?",
 o:["Running the calculation for many people at the level of society","The idea that pleasure and pain exist","The idea that individuals can calculate their own balance"],c:0,
 r:"The difficulties arise when the calculus is made at the scale of society, or globally."}
];
```

---

## Point 5. Bentham's three convictions (progress 25%)

Why did Bentham build the theory this way? He lived through the French Revolution and the writing of the American constitution, which put freedom and equality at the center of public life, and he wanted ethics to match. So he held three convictions. Everybody counts for one, so each person's pain and pleasure deserves equal moral consideration, which was revolutionary at the time. Pleasure over pain is the ultimate good, a basic biological fact that needs no further justification. And morality must be predictable and calculable, so that in every situation there is one right answer rather than taste, inconsistency or prejudice.

**Visual** (`p5_visual.html`): three cards: Equality, Ultimate good, Calculable.

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 330" xmlns="http://www.w3.org/2000/svg">
<rect width="760" height="330" fill="#111"/>
<text x="380" y="28" text-anchor="middle" fill="#eee" font-size="16" font-weight="700">Bentham's three convictions</text>
<g>
<rect x="15" y="50" width="235" height="260" rx="12" fill="#222" stroke="#888"/>
<text x="132" y="82" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">1. Equality</text>
<text x="132" y="104" text-anchor="middle" fill="#bbb" font-size="13">everybody counts for one</text>
<g fill="#3a6ea5"><circle cx="70" cy="165" r="20"/><circle cx="132" cy="165" r="20"/><circle cx="194" cy="165" r="20"/></g>
<g fill="#fff" font-size="16" font-weight="700" text-anchor="middle"><text x="70" y="171">1</text><text x="132" y="171">1</text><text x="194" y="171">1</text></g>
<text x="132" y="230" text-anchor="middle" fill="#eee" font-size="13">each person's pain and pleasure</text>
<text x="132" y="250" text-anchor="middle" fill="#eee" font-size="13">gets the same weight</text>
</g>
<g>
<rect x="262" y="50" width="235" height="260" rx="12" fill="#222" stroke="#888"/>
<text x="380" y="82" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">2. Ultimate good</text>
<text x="380" y="104" text-anchor="middle" fill="#bbb" font-size="13">pleasure over pain</text>
<rect x="320" y="135" width="120" height="50" rx="8" fill="#1f7a3d"/>
<text x="380" y="166" text-anchor="middle" fill="#fff" font-size="15" font-weight="700">pleasure − pain</text>
<text x="380" y="230" text-anchor="middle" fill="#eee" font-size="13">a basic biological fact,</text>
<text x="380" y="250" text-anchor="middle" fill="#eee" font-size="13">no further argument needed</text>
</g>
<g>
<rect x="510" y="50" width="235" height="260" rx="12" fill="#222" stroke="#888"/>
<text x="627" y="82" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">3. Calculable</text>
<text x="627" y="104" text-anchor="middle" fill="#bbb" font-size="13">a principle you can count on</text>
<text x="627" y="160" text-anchor="middle" fill="#6fdc8c" font-size="14">predictable · consistent</text>
<text x="627" y="182" text-anchor="middle" fill="#ff8a80" font-size="14">not taste · not prejudice</text>
<text x="627" y="230" text-anchor="middle" fill="#eee" font-size="13">one good answer</text>
<text x="627" y="250" text-anchor="middle" fill="#eee" font-size="13">in every situation</text>
</g>
</svg></body></html>
```

The three cards are connected: equality tells you whose pleasure and pain to count (everyone's, with equal weight), the ultimate good tells you what to count, and calculability tells you how to count it, namely by a rule and not by gut feeling.

> **Takeaway:** Bentham counts everyone equally, takes pleasure over pain as the ultimate good, and demands a calculable principle instead of taste or prejudice.

**Quiz** (`p5_quiz.html`):

```javascript
const Q=[
{p:"What does \"everybody counts for one\" mean?",
 o:["Each person\'s pain and pleasure gets equal moral consideration","Only one person\'s happiness can be counted per decision","Everyone has exactly one pleasure"],c:0,
 r:"Equal weight for every person, which was revolutionary in Bentham\'s time."},
{p:"Why does Bentham say pleasure over pain is the ultimate good?",
 o:["He derived it from a religious principle","It is a basic biological fact, so no further argument or justification is needed","Because most people vote for it"],c:1,
 r:"An ultimate principle cannot be derived from anything else, it is simply how human beings feel."},
{p:"Which would Bentham reject as the basis of morality?",
 o:["A principle that is predictable and calculable","A principle giving one good answer in every situation","A principle based on personal taste or prejudice"],c:2,
 r:"Morality must not be taste, inconsistent, or based on prejudice or corruption."}
];
```

---

## Point 6. Bentham's proof by elimination: asceticism

How do you prove that utilitarianism is the true moral theory? Strikingly, Bentham has no direct argument for it. He gives an indirect proof: show what is wrong with every alternative, and what remains must be accepted. Rawls reasons the same way in his original position, where utilitarianism is one of the opponents he knocks out. The first alternative Bentham knocks out is asceticism, the view that you should subject yourself to pain on earth, because suffering is what earns you eternal pleasure in the afterlife.

**Visual** (`p6_visual.html`): three cards: Asceticism (crossed out with three reasons), Sympathy (next point), Utility principle (what remains).

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 340" xmlns="http://www.w3.org/2000/svg">
<rect width="760" height="340" fill="#111"/>
<text x="380" y="26" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Proof by elimination: knock out the rivals, what is left must be accepted</text>
<rect x="20" y="50" width="225" height="270" rx="12" fill="#222" stroke="#b3261e" stroke-width="2"/>
<text x="132" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Asceticism</text>
<text x="132" y="100" text-anchor="middle" fill="#bbb" font-size="12">suffer now, eternal pleasure later</text>
<g font-size="12.5" fill="#eee">
<text x="34" y="135">✗ Maximizes pain on earth</text>
<text x="34" y="156">  with no good justification</text>
<text x="34" y="190">✗ If you count the afterlife,</text>
<text x="34" y="211">  it is just a utility principle:</text>
<text x="34" y="232">  short pain for infinite pleasure</text>
<text x="34" y="266">✗ Harmful consequences</text>
<text x="34" y="287">  (e.g. a ban on contraception)</text>
</g>
<rect x="268" y="50" width="225" height="270" rx="12" fill="#222" stroke="#888" stroke-dasharray="6 4"/>
<text x="380" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Sympathy</text>
<text x="380" y="100" text-anchor="middle" fill="#bbb" font-size="12">decide by empathy</text>
<text x="380" y="200" text-anchor="middle" fill="#bbb" font-size="14">next point</text>
<rect x="516" y="50" width="225" height="270" rx="12" fill="#1f7a3d"/>
<text x="628" y="80" text-anchor="middle" fill="#fff" font-size="15" font-weight="700">Utility principle</text>
<text x="628" y="100" text-anchor="middle" fill="#fff" font-size="12">what remains</text>
<text x="628" y="200" text-anchor="middle" fill="#fff" font-size="13">no direct argument,</text>
<text x="628" y="220" text-anchor="middle" fill="#fff" font-size="13">only "the others fail"</text>
</svg></body></html>
```

Even on its own terms, the ascetic's reason for suffering is utility: accept a short time of pain to get infinite happiness. So asceticism is a utility principle that was never presented as one. It also caused much suffering in practice. The lecture gives a ban on contraception as an example of such a customary rule leading to bad consequences, but the transcript is unclear about whose critique that was, so treat the example as illustrative.

> **Takeaway:** Bentham has no direct proof of utilitarianism, only proof by elimination, and asceticism fails because it has no justification of its own, hides a utility principle, and causes needless suffering.

**Quiz** (`p6_quiz.html`):

```javascript
const Q=[
{p:"What kind of argument does Bentham give for utilitarianism?",
 o:["An indirect proof: the alternatives fail, so utilitarianism remains","A direct proof from first principles","An appeal to what religion teaches"],c:0,
 r:"He has no direct argument, only a game of elimination of the alternatives."},
{p:"What is the ascetic principle?",
 o:["Maximize pleasure on earth","Suffer on earth to earn eternal pleasure in the afterlife","Decide by sympathy for the person affected"],c:1,
 r:"Asceticism subjects you to pain now for an afterlife reward."},
{p:"Why does Bentham say asceticism is secretly a principle of utility?",
 o:["It accepts a short time of suffering for infinite happiness, which is a pleasure-over-pain trade","It forbids all pleasure","It counts everyone\'s pleasure equally"],c:0,
 r:"Including the afterlife, the goal is still the maximum happiness over pain."}
];
```

---

## Point 7. The second rival: deciding by sympathy

The other alternative Bentham eliminates is the principle of sympathy or empathy: make ethical decisions on the basis of your sympathy for the people involved. Take the lecture's example. Your sister's birthday party falls at the same time as your friend's house move, and you promised to help. Sympathy gives you no scale to weigh the two, so the decision is a gut reaction.

**Visual** (`p7_visual.html`): the same dilemma decided by sympathy (no principle, no way to question, no accountability) versus by the utilitarian calculus (formula, checkable, accountable).

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 330" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="330" fill="#111"/>
<text x="380" y="26" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Dilemma: sister's birthday party or helping a friend move?</text>
<rect x="20" y="50" width="340" height="260" rx="12" fill="#222" stroke="#b3261e" stroke-width="2"/>
<text x="190" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Sympathy</text>
<rect x="50" y="100" width="280" height="44" rx="8" fill="#333"/>
<text x="190" y="127" text-anchor="middle" fill="#eee" font-size="14">gut reaction</text>
<line x1="190" y1="144" x2="190" y2="170" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<rect x="50" y="172" width="280" height="44" rx="8" fill="#333"/>
<text x="190" y="199" text-anchor="middle" fill="#eee" font-size="14">decision</text>
<g font-size="12.5" fill="#ff8a80"><text x="40" y="244">✗ no principle or formula to guide you</text><text x="40" y="266">✗ nobody can question the result</text><text x="40" y="288">✗ no accountability</text></g>
<rect x="400" y="50" width="340" height="260" rx="12" fill="#222" stroke="#1f7a3d" stroke-width="2"/>
<text x="570" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Utilitarian calculus</text>
<rect x="430" y="100" width="280" height="44" rx="8" fill="#333"/>
<text x="570" y="127" text-anchor="middle" fill="#eee" font-size="14">weigh good and bad of each option</text>
<line x1="570" y1="144" x2="570" y2="170" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<rect x="430" y="172" width="280" height="44" rx="8" fill="#333"/>
<text x="570" y="199" text-anchor="middle" fill="#eee" font-size="14">decision</text>
<g font-size="12.5" fill="#6fdc8c"><text x="420" y="244">✓ a formula you can follow</text><text x="420" y="266">✓ others can check or dispute your steps</text><text x="420" y="288">✓ you can be held accountable</text></g>
</svg></body></html>
```

The two columns have the same input and differ only in how the decision is reached. With sympathy, nobody can question whether you did the right thing, so there is no accountability. Bentham wanted ethics that works like science, with an almost mathematical calculus that gives people a procedure they can follow and others can check.

> **Takeaway:** deciding by sympathy gives no principle, no way to question the result and no accountability, which is why Bentham wanted a calculable theory instead.

**Quiz** (`p7_quiz.html`):

```javascript
const Q=[
{p:"What is Bentham\'s main objection to deciding by sympathy?",
 o:["Sympathy always leads to harm","It gives no principle or formula, so no one can check or question the decision","Sympathy is only felt by humans"],c:1,
 r:"The decision is left to your own intuition, with no external standard and no accountability."},
{p:"Why does the calculus give accountability that sympathy lacks?",
 o:["Because its steps are laid out, so others can examine and dispute them","Because it always gives the answer people like","Because it removes all disagreement"],c:0,
 r:"A structured procedure can be inspected step by step."},
{p:"Which pair is correctly matched?",
 o:["Asceticism: decide by empathy","Sympathy: suffer now for eternal pleasure","Sympathy: a gut reaction without a scale to weigh the options"],c:2,
 r:"Asceticism is suffering for an afterlife reward, sympathy is the gut-reaction principle."}
];
```

---

## Point 8. First criticism: "pleasure" is too broad

Now the objections start. The first says that if the ultimate good is simply pleasure, the calculation lets in too much. What if someone takes pleasure in another person's misfortune, for example someone who enjoys seeing a person break a leg? On a pure pleasure-and-pain count, that pleasure goes into the sum. Should it? And should all pleasures weigh the same? Mill, Bentham's follower, thought not: a theory in which all pleasures are equal is, in the words of the critics, a philosophy suitable for pigs, since animals also only feel pleasure and pain. He wanted a hierarchy of higher and lower pleasures.

**Visual** (`p8_visual.html`): three pleasures (seeing someone break a leg, arm wrestling, piano or opera) flowing into "the sum", with Problem 1 and Problem 2.

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 340" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="340" fill="#111"/>
<text x="20" y="28" fill="#bbb" font-size="13">Everything that feels good goes into the sum ...</text>
<rect x="20" y="45" width="300" height="52" rx="8" fill="#222" stroke="#888"/>
<text x="170" y="76" text-anchor="middle" fill="#eee" font-size="14">pleasure at seeing someone break a leg</text>
<rect x="20" y="115" width="300" height="52" rx="8" fill="#222" stroke="#888"/>
<text x="170" y="146" text-anchor="middle" fill="#eee" font-size="14">pleasure of arm wrestling</text>
<rect x="20" y="185" width="300" height="52" rx="8" fill="#222" stroke="#888"/>
<text x="170" y="216" text-anchor="middle" fill="#eee" font-size="14">pleasure of playing piano, going to the opera</text>
<g stroke="#aaa" stroke-width="2" marker-end="url(#a)"><line x1="320" y1="71" x2="400" y2="140"/><line x1="320" y1="141" x2="400" y2="160"/><line x1="320" y1="211" x2="400" y2="180"/></g>
<rect x="405" y="105" width="140" height="95" rx="12" fill="#1f7a3d"/>
<text x="475" y="145" text-anchor="middle" fill="#fff" font-size="15" font-weight="700">The sum</text>
<text x="475" y="168" text-anchor="middle" fill="#fff" font-size="12">all equal?</text>
<text x="650" y="75" text-anchor="middle" fill="#ff8a80" font-size="13" font-weight="700">Problem 1</text>
<text x="650" y="95" text-anchor="middle" fill="#eee" font-size="12.5">Should bad pleasures count?</text>
<text x="650" y="115" text-anchor="middle" fill="#eee" font-size="12.5">Distinguish good from bad,</text>
<text x="650" y="135" text-anchor="middle" fill="#eee" font-size="12.5">but on what basis?</text>
<text x="650" y="195" text-anchor="middle" fill="#ff8a80" font-size="13" font-weight="700">Problem 2</text>
<text x="650" y="215" text-anchor="middle" fill="#eee" font-size="12.5">Mill: higher vs lower pleasures</text>
<text x="650" y="235" text-anchor="middle" fill="#eee" font-size="12.5">Bentham: no hierarchy</text>
<text x="380" y="300" text-anchor="middle" fill="#bbb" font-size="12.5">Today a ranking of pleasures can sound elitist or anti-democratic, but that was the debate.</text>
</svg></body></html>
```

The attribution in the lecture is loose: it presents the "which pleasures count, and are they equal?" question as a debate between Mill and Bentham, so the hierarchy is described as Mill's position and "all pleasures equal" as Bentham's original. If you separate good pleasures from bad ones, you need some standard beyond pleasure itself to do it, and that standard is exactly what the theory was trying to avoid.

> **Takeaway:** the first objection is that "pleasure" is too broad, since it lets in pleasures like enjoying others' misfortune, and ranking pleasures into higher and lower needs a standard that goes beyond pleasure itself.

**Quiz** (`p8_quiz.html`):

```javascript
const Q=[
{p:"What is the \"too broad\" objection to counting pleasure?",
 o:["A pure pleasure count includes pleasures we would not want in an ethical theory, like enjoying another\'s misfortune","Pleasure is too hard to feel","Only humans feel pleasure"],c:0,
 r:"If all pleasure counts, even pleasure in someone\'s suffering goes into the sum."},
{p:"Why do critics say the original theory suits pigs?",
 o:["Pigs are more moral than humans","Animals also only feel pleasure and pain, so humans would be no different morally","Because it forbids eating"],c:1,
 r:"If only pleasure and pain count, nothing distinguishes human pleasures from animal ones."},
{p:"What was Mill\'s move in response?",
 o:["Count only physical pleasures","Drop pleasure and count only duty","Rank pleasures into higher ones (piano, opera) and lower ones"],c:2,
 r:"A hierarchy of pleasures, though it can sound elitist today."}
];
```

### Your question: did Mill count "pleasure in hurting someone" as a smaller number?

That is not something the lecture says, and the diagram may have suggested it. The lecture raises two separate questions. (1) Should pleasure taken in someone else's misfortune count at all? The lecture asks this and leaves it open; it does not say how Mill answers it. (2) Are all pleasures equal? Here Mill comes in: he wanted a hierarchy of higher and lower pleasures (arm wrestling versus piano or opera) in answer to the "philosophy for pigs" objection. So a "smaller number" for malicious pleasure is a natural way to combine the two, but it is not in the lecture. The diagram placed the two problems next to each other, and Mill's hierarchy only belongs to Problem 2.

You then asked: *so he just raised the question?* Yes, as far as the lecture goes: the lecturer raised the question about malicious pleasure and left it open. The only thing attributed to Mill here is the higher and lower pleasures hierarchy.

---

## Point 9. Second criticism: "pleasure and pain" is too narrow

The opposite objection says the theory leaves out too much. Reducing morality to pleasure and pain, simple biological facts, seems too small a basis for ethics. Many of the most worthwhile things in life are hard and painful while you pursue them: becoming a world-class piano player, chess player or brain surgeon. The lecturer's own example is John Rawls, who spent about 30 years on his theory of justice, a lonely road full of self-doubt, and what he left behind seems worth it.

**Visual** (`p9_visual.html`): a curve over time: a long red stretch of pain and doubt, then a green stretch of result and life satisfaction (the curve is an illustration, not from the lecture).

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 340" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="340" fill="#111"/>
<text x="380" y="24" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">A worthwhile, difficult project (e.g. writing a major book)</text>
<line x1="70" y1="170" x2="720" y2="170" stroke="#888" stroke-width="1.5" marker-end="url(#a)"/>
<line x1="70" y1="50" x2="70" y2="300" stroke="#888" stroke-width="1.5" marker-end="url(#a)"/>
<text x="715" y="190" text-anchor="end" fill="#bbb" font-size="12">time</text>
<text x="76" y="62" fill="#bbb" font-size="12">pleasure (+)</text>
<text x="76" y="296" fill="#bbb" font-size="12">pain (−)</text>
<path d="M70,175 C130,220 180,260 260,255 C340,250 400,240 470,225 C540,205 580,150 640,100 C670,80 690,75 710,72" fill="none" stroke="#eee" stroke-width="3"/>
<path d="M70,170 L70,175 C130,220 180,260 260,255 C340,250 400,240 470,225 L470,170 Z" fill="#b3261e" opacity="0.55"/>
<path d="M470,170 L470,225 C540,205 580,150 640,100 C670,80 690,75 710,72 L710,170 Z" fill="#1f7a3d" opacity="0.55"/>
<text x="270" y="290" text-anchor="middle" fill="#ff8a80" font-size="13">years of hard work, doubt, loneliness</text>
<text x="620" y="140" text-anchor="middle" fill="#6fdc8c" font-size="13">the result, life satisfaction</text>
<text x="380" y="325" text-anchor="middle" fill="#bbb" font-size="12.5">Judged moment by moment, the long red stretch looks bad. Is the project worthwhile only if the total comes out positive?</text>
</svg></body></html>
```

The critics' claim is that the worth of such a life project cannot be captured by summing pleasure and pain. The lecture's wording is that it "doesn't make sense" to characterize these projects as a balance of pleasure or pain. Note how this mirrors the previous point: the first objection said the sum lets in too much, this one says the sum misses what makes some difficult goals valuable.

> **Takeaway:** the "too narrow" objection says that reducing ethics to pleasure and pain misses the value of hard, painful projects, whose worth shows only in the result.

**Quiz** (`p9_quiz.html`):

```javascript
const Q=[
{p:"What does the \"too narrow\" objection claim?",
 o:["Pleasure lets in bad pleasures","Reducing morality to pleasure and pain leaves out the value of hard goals","Only a few people can feel pleasure"],c:1,
 r:"Many worthwhile pursuits are painful along the way, so a pleasure-pain sum misses their worth."},
{p:"Why does the Rawls example fit the objection?",
 o:["He enjoyed every moment of the work","He wrote the book quickly","He spent about 30 years on a lonely, doubt-filled project that seems worthwhile anyway"],c:2,
 r:"The hard work would count as pain, yet the result seems worth it."},
{p:"How does this objection differ from the \"too broad\" one?",
 o:["Too broad: the sum includes too much. Too narrow: it leaves out what makes hard projects worthwhile","They are the same objection","Too broad is about animals, too narrow is about humans"],c:0,
 r:"One says the sum lets in too much, the other that it misses too much."}
];
```

---

## Point 10. How do we measure pain and pleasure? (progress 50%)

The calculation only works if we know what to count. Bentham already named factors that matter for a pain or pleasure, some obvious and some controversial. Intensity is how severe it is. Duration is how long it lasts: a 10-second shock and two days of torture differ in both. Certainty, which we would now call probability, matters because we are always judging outcomes that may not happen. A fourth factor, remoteness, gets its own point next.

**Visual** (`p10_visual.html`): four cards: Intensity, Duration, Certainty, Remoteness (dashed, "next point").

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 320" xmlns="http://www.w3.org/2000/svg">
<rect width="760" height="320" fill="#111"/>
<text x="380" y="26" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">What weighs in on a pain or pleasure (Bentham's factors)</text>
<g>
<rect x="15" y="50" width="175" height="240" rx="12" fill="#222" stroke="#888"/>
<text x="102" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Intensity</text>
<text x="102" y="100" text-anchor="middle" fill="#bbb" font-size="12">how severe?</text>
<rect x="55" y="170" width="20" height="30" fill="#b3261e" opacity="0.6"/><rect x="85" y="140" width="20" height="60" fill="#b3261e" opacity="0.8"/><rect x="115" y="110" width="20" height="90" fill="#b3261e"/>
<text x="102" y="250" text-anchor="middle" fill="#eee" font-size="12">mild pain vs severe pain</text>
</g>
<g>
<rect x="200" y="50" width="175" height="240" rx="12" fill="#222" stroke="#888"/>
<text x="287" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Duration</text>
<text x="287" y="100" text-anchor="middle" fill="#bbb" font-size="12">how long?</text>
<rect x="225" y="150" width="20" height="50" fill="#b3261e"/><rect x="225" y="170" width="120" height="30" fill="#b3261e" opacity="0.5"/>
<text x="287" y="235" text-anchor="middle" fill="#eee" font-size="12">10 seconds of shock</text>
<text x="287" y="255" text-anchor="middle" fill="#eee" font-size="12">vs two days of torture</text>
</g>
<g>
<rect x="385" y="50" width="175" height="240" rx="12" fill="#222" stroke="#888"/>
<text x="472" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Certainty</text>
<text x="472" y="100" text-anchor="middle" fill="#bbb" font-size="12">how likely?</text>
<text x="472" y="170" text-anchor="middle" fill="#eee" font-size="28" font-weight="700">p</text>
<text x="472" y="235" text-anchor="middle" fill="#eee" font-size="12">the probability the pain or</text>
<text x="472" y="255" text-anchor="middle" fill="#eee" font-size="12">pleasure will occur at all</text>
</g>
<g>
<rect x="570" y="50" width="175" height="240" rx="12" fill="#222" stroke="#888" stroke-dasharray="6 4"/>
<text x="657" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Remoteness</text>
<text x="657" y="100" text-anchor="middle" fill="#bbb" font-size="12">how far away?</text>
<text x="657" y="170" text-anchor="middle" fill="#bbb" font-size="14">in space and in time</text>
<text x="657" y="235" text-anchor="middle" fill="#bbb" font-size="12">next point</text>
</g>
</svg></body></html>
```

The three solid cards are the factors that are easy to accept. The lecture says some of Bentham's factors are obvious and others become controversial, and the dashed card is the controversial one. The bars in the intensity and duration cards are only an illustration of the idea.

> **Takeaway:** to count a pain or pleasure, Bentham weighs its intensity (how severe), its duration (how long) and its certainty (how probable), and a fourth factor, remoteness, is more controversial.

**Quiz** (`p10_quiz.html`):

```javascript
const Q=[
{p:"Which factor is about how likely a pain or pleasure is to occur at all?",
 o:["Intensity","Certainty","Duration"],c:1,
 r:"Certainty is what we would now call probability, since we always judge outcomes that might not happen."},
{p:"A 10-second shock and two days of torture differ in which factors?",
 o:["Only in certainty","Only in remoteness","Both in intensity and in duration"],c:2,
 r:"The lecture says they are very different both in intensity and in duration."},
{p:"Which factor measures how severe a pain is?",
 o:["Intensity","Remoteness","Duration"],c:0,
 r:"Intensity is severity, duration is how long it lasts."}
];
```

---

## Point 11. Remoteness: does distance change how much someone counts?

The fourth factor asks whether a pain or pleasure counts less when it is far away, in space or in time. Bentham's answer for space is that distance should not matter to our obligations to others: a person far away counts the same as one next to us. This sets up Peter Singer later today. For time, the issue is discounting the future. Policy makers tend to give less weight to future consequences, which shows clearly in climate change policy, where today's decisions affect generations far down the line.

**Visual** (`p11_visual.html`): weight given (y) against distance away (x): a flat green line (every person counts for one) and a falling red curve (discounting). The axes and curves are a sketch, not a figure from the lecture.

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 330" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="330" fill="#111"/>
<text x="380" y="24" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">How much weight does a person's wellbeing get?</text>
<line x1="80" y1="260" x2="700" y2="260" stroke="#888" stroke-width="1.5" marker-end="url(#a)"/>
<line x1="80" y1="260" x2="80" y2="45" stroke="#888" stroke-width="1.5" marker-end="url(#a)"/>
<text x="700" y="282" text-anchor="end" fill="#bbb" font-size="12">distance away (in space, or in time into the future)</text>
<text x="90" y="52" fill="#bbb" font-size="12">weight given</text>
<line x1="80" y1="90" x2="690" y2="90" stroke="#1f7a3d" stroke-width="4"/>
<text x="690" y="78" text-anchor="end" fill="#6fdc8c" font-size="13" font-weight="700">Utilitarian ideal: every person counts for one</text>
<path d="M80,90 C200,150 300,205 690,245" fill="none" stroke="#b3261e" stroke-width="4"/>
<text x="500" y="195" fill="#ff8a80" font-size="13" font-weight="700">Discounting: further away, less weight</text>
<text x="80" y="305" fill="#bbb" font-size="12">Space: Bentham says distance should not matter to our obligations.  Time: discounting future generations is a problem for utilitarianism.</text>
</svg></body></html>
```

The flat green line is what utilitarianism, with its equal consideration for everyone, would demand. The falling red line is what discounting does: just because people live further in the future, their happiness gets weighed less. The lecture calls this problematic for utilitarianism. It adds that it is a further question whether people who already exist and people not yet born should be treated the same, and does not settle it.

> **Takeaway:** for utilitarianism, distance should not reduce the weight of someone's wellbeing, whether the distance is in space (Bentham) or in time (discounting future generations is problematic).

**Quiz** (`p11_quiz.html`):

```javascript
const Q=[
{p:"What does \"discounting the future\" mean?",
 o:["Giving less weight to the wellbeing of people the further in the future they live","Making future products cheaper","Counting future pleasure twice"],c:0,
 r:"Future consequences get weighed less just because they lie further away in time."},
{p:"What is Bentham\'s view on distance in space?",
 o:["Obligations are strongest to people nearby","Distance should not matter to our obligations to others","Only citizens of our own country count"],c:1,
 r:"This is the view that Singer picks up later in the lecture."},
{p:"Where does the lecture say discounting shows up in practice?",
 o:["Hospital waiting lists","Choosing a school sports facility","Climate change policy"],c:2,
 r:"The effects of today\'s decisions fall on many generations down the line."}
];
```

---

## Point 12. Comparing people: does your 7 equal my 7?

To add up everyone's pleasure and pain we need a scale, so that each person's pleasure or pain can be assigned a number, and then we need to compare the numbers of different people. The trouble is that two people can report the same number under very different circumstances. Say you and I both rate our happiness at seven out of ten. My seven may come from a miserable life where I cannot imagine a better world, while your seven comes from feeling well but sensing you have much more potential.

**Visual** (`p12_visual.html`): Person A and Person B both report 7/10, with different reasons behind the number and "=?" between them.

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 330" xmlns="http://www.w3.org/2000/svg">
<rect width="760" height="330" fill="#111"/>
<text x="380" y="26" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Same report, different meaning</text>
<rect x="20" y="45" width="345" height="265" rx="12" fill="#222" stroke="#888"/>
<text x="192" y="75" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Person A reports</text>
<rect x="147" y="90" width="90" height="60" rx="10" fill="#3a6ea5"/>
<text x="192" y="132" text-anchor="middle" fill="#fff" font-size="30" font-weight="700">7/10</text>
<text x="192" y="180" text-anchor="middle" fill="#bbb" font-size="12">what is behind the number:</text>
<text x="192" y="205" text-anchor="middle" fill="#eee" font-size="13">a hard life, but no vision of</text>
<text x="192" y="225" text-anchor="middle" fill="#eee" font-size="13">any better alternative</text>
<text x="192" y="270" text-anchor="middle" fill="#ff8a80" font-size="13" font-weight="700">adaptive preferences</text>
<rect x="395" y="45" width="345" height="265" rx="12" fill="#222" stroke="#888"/>
<text x="567" y="75" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Person B reports</text>
<rect x="522" y="90" width="90" height="60" rx="10" fill="#3a6ea5"/>
<text x="567" y="132" text-anchor="middle" fill="#fff" font-size="30" font-weight="700">7/10</text>
<text x="567" y="180" text-anchor="middle" fill="#bbb" font-size="12">what is behind the number:</text>
<text x="567" y="205" text-anchor="middle" fill="#eee" font-size="13">a good life, but a sense of</text>
<text x="567" y="225" text-anchor="middle" fill="#eee" font-size="13">more potential still to reach</text>
<text x="380" y="190" text-anchor="middle" fill="#fff" font-size="26" font-weight="700">=?</text>
</svg></body></html>
```

Person A's number is an example of adaptive preferences, a serious problem in welfare economics: people adjust what they expect to their circumstances, so their self-reported satisfaction can be high even when their situation is objectively poor. The lecture gives a real-world version. When people in very poor countries are asked about their life satisfaction, the answers are much higher than objective measures of poverty would predict, and objective comparisons rank those countries very low. So it is unclear what the number measures and how to compare it.

> **Takeaway:** to add up wellbeing we must compare different people's numbers, but the same reported number can hide very different circumstances (adaptive preferences), so the comparison is not straightforward.

**Quiz** (`p12_quiz.html`):

```javascript
const Q=[
{p:"What do adaptive preferences mean here?",
 o:["People adjust what they expect to their circumstances, so reported satisfaction can be high despite poor conditions","People change their vote often","People prefer what is cheaper"],c:0,
 r:"The same reported number can hide very different circumstances and expectations."},
{p:"Why is comparing two people\'s reported 7/10 a problem for the utilitarian calculation?",
 o:["Because 7 is a bad score","Because the number may mean different things in different circumstances","Because nobody can report a number"],c:1,
 r:"To sum wellbeing across people we need numbers that are comparable."},
{p:"What does the lecture report about life satisfaction in poor countries?",
 o:["It is much lower than objective poverty measures suggest","It matches objective measures exactly","It is higher than objective measures would predict"],c:2,
 r:"Subjective satisfaction is relatively high even though the countries rank low on objective measures."}
];
```

---

## Point 13. Mill applies the calculation: the subjection of women

Mill was Bentham's follower who improved the theory, a great public promoter of utilitarianism, and in the lecture's words the first feminist philosopher of his time. His 1869 pamphlet on the subjection of women applies the utilitarian calculation to the morality of his own society (the transcript says "matriarchal", clearly a slip for patriarchal). A married woman could not vote, hold office, enter most professions or educational institutions, or inherit property, and she depended on her husband. Mill thought marriage effectively meant slavery for a woman.

**Visual** (`p13_visual.html`): Option 1 (the current situation, with its restrictions) compared with Option 2 (liberate women).

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 330" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="330" fill="#111"/>
<text x="380" y="26" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Mill's method: compare two scenarios by their consequences</text>
<rect x="20" y="50" width="320" height="250" rx="12" fill="#222" stroke="#b3261e" stroke-width="2"/>
<text x="180" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Option 1: the current situation</text>
<g font-size="13" fill="#eee"><text x="45" y="125">✗ women cannot vote or hold office</text><text x="45" y="150">✗ banned from most professions</text><text x="45" y="175">✗ barred from educational opportunities</text><text x="45" y="200">✗ cannot inherit property</text><text x="45" y="225">✗ dependent on the husband</text></g>
<text x="180" y="270" text-anchor="middle" fill="#bbb" font-size="12">men are sole breadwinner and leader of the family</text>
<rect x="420" y="50" width="320" height="250" rx="12" fill="#222" stroke="#1f7a3d" stroke-width="2"/>
<text x="580" y="80" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Option 2: liberate women</text>
<g font-size="13" fill="#eee"><text x="445" y="125">✓ open all education to women</text><text x="445" y="150">✓ open all professions to women</text><text x="445" y="175">✓ equal legal standing and rights</text></g>
<text x="580" y="270" text-anchor="middle" fill="#bbb" font-size="12">compare the consequences of 1 and 2</text>
<line x1="345" y1="175" x2="415" y2="175" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<line x1="415" y1="195" x2="345" y2="195" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
</svg></body></html>
```

This is the same procedure as in point 3: list the options, then compare their consequences. Mill claims that subjection is bad from every point of view, for men, for women and for society as a whole. Note that he was not popular at the time: he was a member of Parliament, and these were very radical ideas then.

> **Takeaway:** Mill applies the utilitarian method to a real social question by comparing the consequences of keeping women's subjection with those of liberating women.

**Quiz** (`p13_quiz.html`):

```javascript
const Q=[
{p:"What is Mill\'s method in his argument on the subjection of women?",
 o:["Appeal to the natural character of men and women","Compare the consequences of the current situation with those of liberating women","Appeal to religious tradition"],c:1,
 r:"It is the utilitarian comparison of options by their consequences."},
{p:"From whose point of view does Mill claim subjection is bad?",
 o:["Men, women and society as a whole","Women only","Society only"],c:0,
 r:"He argues it is detrimental from every point of view, not only women\'s."},
{p:"What is the relation between Mill and Bentham in the lecture?",
 o:["Mill rejected utilitarianism","Mill was Bentham\'s follower who promoted and improved the theory","Mill lived before Bentham"],c:1,
 r:"Philosophical students build on their predecessors and, when they succeed, improve the theory."}
];
```

---

## Point 14. Three arguments: everyone is worse off (progress 75%)

Mill's claim is that the current arrangement leaves everyone worse off, so the comparison is not close. He makes three arguments, one for each point of view. Men: as the sole breadwinner they must secure 100% income for the whole family, so they become more conservative in their choices, becoming a lawyer or doctor rather than an artist. Society: banning women from education and professions wastes half of humanity's talent. Women: they are less happy, constrained and coerced.

**Visual** (`p14_visual.html`): three cards (Men, Society, Women), each "worse off", leading to "Utilitarianism requires liberation".

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 340" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="340" fill="#111"/>
<text x="380" y="24" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Is the current situation better than liberation? From three points of view:</text>
<rect x="15" y="45" width="235" height="190" rx="12" fill="#222" stroke="#888"/>
<text x="132" y="74" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Men</text>
<text x="132" y="104" text-anchor="middle" fill="#eee" font-size="12.5">sole breadwinner for the</text>
<text x="132" y="122" text-anchor="middle" fill="#eee" font-size="12.5">whole family, so they must</text>
<text x="132" y="140" text-anchor="middle" fill="#eee" font-size="12.5">choose safe careers</text>
<text x="132" y="160" text-anchor="middle" fill="#eee" font-size="12.5">(lawyer, doctor, not artist)</text>
<text x="132" y="205" text-anchor="middle" fill="#ff8a80" font-size="14" font-weight="700">less well off</text>
<rect x="262" y="45" width="235" height="190" rx="12" fill="#222" stroke="#888"/>
<text x="380" y="74" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Society</text>
<text x="380" y="104" text-anchor="middle" fill="#eee" font-size="12.5">women excluded from education</text>
<text x="380" y="122" text-anchor="middle" fill="#eee" font-size="12.5">and professions, so half of</text>
<text x="380" y="140" text-anchor="middle" fill="#eee" font-size="12.5">humanity's talent is wasted</text>
<text x="380" y="205" text-anchor="middle" fill="#ff8a80" font-size="14" font-weight="700">worse off</text>
<rect x="510" y="45" width="235" height="190" rx="12" fill="#222" stroke="#888"/>
<text x="627" y="74" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Women</text>
<text x="627" y="104" text-anchor="middle" fill="#eee" font-size="12.5">constrained and coerced,</text>
<text x="627" y="122" text-anchor="middle" fill="#eee" font-size="12.5">their happiness is much</text>
<text x="627" y="140" text-anchor="middle" fill="#eee" font-size="12.5">lower than it could be</text>
<text x="627" y="205" text-anchor="middle" fill="#ff8a80" font-size="14" font-weight="700">worse off</text>
<g stroke="#aaa" stroke-width="2" marker-end="url(#a)"><line x1="132" y1="238" x2="330" y2="278"/><line x1="380" y1="238" x2="380" y2="274"/><line x1="627" y1="238" x2="430" y2="278"/></g>
<rect x="215" y="282" width="330" height="46" rx="10" fill="#1f7a3d"/>
<text x="380" y="310" text-anchor="middle" fill="#fff" font-size="14" font-weight="700">Utilitarianism requires liberation</text>
</svg></body></html>
```

Since men, women and the collective are all worse off under the current arrangement, the lecture calls this an overwhelming case that utilitarianism requires liberation. The lecture notes that the arguments defenders of subjection offered were very few and rested on the nature of human beings, for example Aristotle's claim about the higher soul of men and the body-versus-brain split, and later medieval theologians' claims about natural leadership. Mill used the same structure against the death penalty, but the lecturer leaves that argument for you to read on your own.

> **Takeaway:** Mill shows by the utilitarian comparison that subjecting women makes men, women and society all worse off, so utilitarianism requires liberation.

**Quiz** (`p14_quiz.html`):

```javascript
const Q=[
{p:"Which argument says women\'s exclusion wastes talent?",
 o:["The argument from the point of view of men","The argument from the point of view of society","The argument from the point of view of women"],c:1,
 r:"Half of humanity is practically excluded from contributing to the societal good."},
{p:"Why does Mill say men are worse off under the current arrangement?",
 o:["They have to work fewer hours","They lose the vote","As sole breadwinner they must choose safe careers, such as lawyer or doctor, instead of becoming an artist"],c:2,
 r:"The whole family depends on one income, so men become conservative in their choices."},
{p:"What is the conclusion of the three arguments together?",
 o:["Men gain and women lose, so the total is unclear","Everyone is worse off, so utilitarianism requires liberation","Only women are worse off"],c:1,
 r:"Men, women and the collective are all worse off, so the comparison clearly favors liberation."}
];
```

---

## Point 15. Mill's proof of utilitarianism, and the flaw in it

Mill wanted a better proof than Bentham's elimination of rivals, one that shows what is fundamentally valuable. He argues by analogy with sight and hearing. The proof that something is visible is that people see it, and the proof that something is audible is that people hear it. By the same pattern, the proof that happiness is desirable is that people desire it. So happiness should be the ultimate principle of morality because it is what people desire.

**Visual** (`p15_visual.html`): the analogy (visible, audible, desirable) and Moore's objection with the two meanings of "desirable".

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 350" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="350" fill="#111"/>
<text x="380" y="24" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Mill's analogy</text>
<g font-size="13" text-anchor="middle">
<rect x="20" y="40" width="220" height="58" rx="8" fill="#222" stroke="#888"/><text x="130" y="64" fill="#eee">visible</text><text x="130" y="84" fill="#bbb" font-size="12">proof: people see it</text>
<rect x="270" y="40" width="220" height="58" rx="8" fill="#222" stroke="#888"/><text x="380" y="64" fill="#eee">audible</text><text x="380" y="84" fill="#bbb" font-size="12">proof: people hear it</text>
<rect x="520" y="40" width="220" height="58" rx="8" fill="#222" stroke="#888"/><text x="630" y="64" fill="#eee">desirable (happiness)</text><text x="630" y="84" fill="#bbb" font-size="12">proof: people desire it</text>
</g>
<text x="380" y="135" text-anchor="middle" fill="#ff8a80" font-size="15" font-weight="700">Moore's objection: "desirable" has two meanings</text>
<rect x="20" y="150" width="340" height="150" rx="12" fill="#222" stroke="#888"/>
<text x="190" y="178" text-anchor="middle" fill="#eee" font-size="14" font-weight="700">1. Capable of being desired</text>
<text x="190" y="205" text-anchor="middle" fill="#eee" font-size="12.5">like visible = capable of being seen</text>
<text x="190" y="230" text-anchor="middle" fill="#eee" font-size="12.5">true of many things, also harmful ones</text>
<text x="190" y="255" text-anchor="middle" fill="#eee" font-size="12.5">that are bad for us or for others</text>
<rect x="400" y="150" width="340" height="150" rx="12" fill="#222" stroke="#1f7a3d" stroke-width="2"/>
<text x="570" y="178" text-anchor="middle" fill="#eee" font-size="14" font-weight="700">2. Ought to be desired</text>
<text x="570" y="205" text-anchor="middle" fill="#eee" font-size="12.5">worth desiring from an ethical point of view</text>
<text x="570" y="230" text-anchor="middle" fill="#eee" font-size="12.5">this is what an ethical principle needs</text>
<text x="380" y="330" text-anchor="middle" fill="#bbb" font-size="12.5">Mill proves meaning 1 (people can desire happiness) but concludes meaning 2 (happiness ought to be desired)</text>
</svg></body></html>
```

G. E. Moore's critique (the transcript writes "Jimmy Moore") is that this is a fallacy of equivocation, the same word used in two meanings, like the fallacies from the methods class at the start of the course. "Visible" means capable of being seen, and the analogy works for that meaning. But "desirable" also means that something ought to be desired. That people can desire something shows only the first meaning, and we often desire things that harm us or others. The lecture adds that Moore was surprised Mill did not see this.

> **Takeaway:** Mill proves happiness is desirable by analogy with sight and hearing, but this slips between "capable of being desired" and "ought to be desired", and ethics needs the second.

**Quiz** (`p15_quiz.html`):

```javascript
const Q=[
{p:"What is Mill\'s argument for happiness as the ultimate principle?",
 o:["Every alternative theory fails","An analogy: visible is shown by people seeing it, so desirable is shown by people desiring it","Religion teaches it"],c:1,
 r:"This replaces Bentham\'s elimination of rivals with an argument by analogy."},
{p:"What is the flaw Moore points out?",
 o:["Happiness cannot be measured","Sight and hearing are not related to desire","\"Desirable\" has two meanings, and the proof only supports the weaker one"],c:2,
 r:"People can desire something, but that does not make it what ought to be desired."},
{p:"Why does it matter that people often desire harmful things?",
 o:["It shows that being capable of being desired does not make something ethically desirable","It shows people never desire happiness","It shows Mill was right"],c:0,
 r:"Capable of being desired holds for harmful things too, so it cannot be the standard of ethics."}
];
```

---

## Point 16. What should we compare: how people feel, or how well off they are?

The Mill and Moore debate points to a discussion that continues among welfare economists today. When we decide how to understand welfare or wellbeing, and what to compare between individuals as the outcome of a policy, there are two options. We can compare what people subjectively perceive, their happiness, pleasure or satisfaction. Or we can compare whether they are objectively better off than in another scenario.

**Visual** (`p16_visual.html`): subjective versus objective wellbeing, each with a plus and a minus (the pros and cons are a tutor extension).

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 330" xmlns="http://www.w3.org/2000/svg">
<rect width="760" height="330" fill="#111"/>
<text x="380" y="26" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Which outcome of a policy should we compare between people?</text>
<rect x="20" y="45" width="345" height="255" rx="12" fill="#222" stroke="#888"/>
<text x="192" y="76" text-anchor="middle" fill="#eee" font-size="16" font-weight="700">Subjective wellbeing</text>
<text x="192" y="110" text-anchor="middle" fill="#eee" font-size="13">how people perceive their own</text>
<text x="192" y="130" text-anchor="middle" fill="#eee" font-size="13">happiness, pleasure, satisfaction</text>
<text x="192" y="175" text-anchor="middle" fill="#6fdc8c" font-size="13">+ measures what the person feels</text>
<text x="192" y="215" text-anchor="middle" fill="#ff8a80" font-size="13">− a 7/10 can mean different things;</text>
<text x="192" y="235" text-anchor="middle" fill="#ff8a80" font-size="13">adaptive preferences</text>
<rect x="395" y="45" width="345" height="255" rx="12" fill="#222" stroke="#888"/>
<text x="567" y="76" text-anchor="middle" fill="#eee" font-size="16" font-weight="700">Objective wellbeing</text>
<text x="567" y="110" text-anchor="middle" fill="#eee" font-size="13">whether people are actually better</text>
<text x="567" y="130" text-anchor="middle" fill="#eee" font-size="13">off than in another scenario</text>
<text x="567" y="175" text-anchor="middle" fill="#6fdc8c" font-size="13">+ not distorted by what people expect</text>
<text x="567" y="215" text-anchor="middle" fill="#ff8a80" font-size="13">− moves away from pleasure and pain</text>
<text x="567" y="235" text-anchor="middle" fill="#ff8a80" font-size="13">(my reading, see text)</text>
</svg></body></html>
```

The lecture only names the two options and says the debate is still alive today. The pros and cons in the diagram are a tutor extension, not from the lecture: the subjective problem comes from point 12 (adaptive preferences), and the objective option's cost, drifting away from pleasure and pain, is my own reading. The link to Moore is that "what people desire" is a subjective standard, while "what ought to be desired" points toward an objective one.

> **Takeaway:** welfare economists still debate whether to compare people by how they subjectively feel or by how objectively well off they are, which is the modern form of the Mill and Moore disagreement.

**Quiz** (`p16_quiz.html`):

```javascript
const Q=[
{p:"Which is the subjective view of wellbeing?",
 o:["Whether people are actually better off than in another scenario","How people perceive their own happiness, pleasure or satisfaction","Income per person in a country"],c:1,
 r:"Subjective means based on how people perceive their own wellbeing."},
{p:"Which problem from earlier points pushes towards an objective measure?",
 o:["Discounting the future","Adaptive preferences, where reported satisfaction can be high despite poor conditions","The refugee shelter example"],c:1,
 r:"If people adapt their expectations, their reports may not show how well off they are. (This link is my extension.)"},
{p:"What does the lecture say about this debate today?",
 o:["It was settled by Moore","It only concerned Bentham","It continues among welfare economists"],c:2,
 r:"The subjective versus objective problem still plays today."}
];
```

---

## Point 17. Singer's argument: does distance matter morally?

Singer starts from a case most of us react to the same way. A two-year-old girl in China is hit by a van and left bleeding in the street, and passers-by walk past her; Singer asks how many in the audience would have stopped to help, and almost everyone says they would have. Then he turns to the numbers: UNICEF reports that in 2011 about 6.9 million children under five died of preventable, poverty-related diseases. That is 19,000 children a day, down from 12 million a year in 1990. His question is whether it makes a morally relevant difference that these children are not right in front of us.

**Visual** (`p17_visual.html`): Singer's argument in four steps (the case, the facts, the key premise in red, what we can do).

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 350" xmlns="http://www.w3.org/2000/svg">
<defs><marker id="a" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto"><path d="M0,0 L10,5 L0,10 z" fill="#aaa"/></marker></defs>
<rect width="760" height="350" fill="#111"/>
<text x="380" y="24" text-anchor="middle" fill="#eee" font-size="15" font-weight="700">Singer's argument in steps</text>
<rect x="20" y="40" width="720" height="52" rx="8" fill="#222" stroke="#888"/>
<text x="380" y="62" text-anchor="middle" fill="#bbb" font-size="12">1. The case in front of you</text>
<text x="380" y="80" text-anchor="middle" fill="#eee" font-size="13.5">A child is dying in front of you: nearly everyone says "I would have stopped to help."</text>
<line x1="380" y1="92" x2="380" y2="112" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<rect x="20" y="114" width="720" height="52" rx="8" fill="#222" stroke="#888"/>
<text x="380" y="136" text-anchor="middle" fill="#bbb" font-size="12">2. The facts</text>
<text x="380" y="154" text-anchor="middle" fill="#eee" font-size="13.5">6.9 million children under five died in 2011 of preventable poverty-related causes (about 19,000 a day)</text>
<line x1="380" y1="166" x2="380" y2="186" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<rect x="20" y="188" width="720" height="52" rx="8" fill="#222" stroke="#b3261e" stroke-width="2"/>
<text x="380" y="210" text-anchor="middle" fill="#ff8a80" font-size="12">3. Key premise</text>
<text x="380" y="228" text-anchor="middle" fill="#eee" font-size="13.5">Distance, nationality or race make no morally relevant difference</text>
<line x1="380" y1="240" x2="380" y2="260" stroke="#aaa" stroke-width="2" marker-end="url(#a)"/>
<rect x="20" y="262" width="720" height="52" rx="8" fill="#222" stroke="#888"/>
<text x="380" y="284" text-anchor="middle" fill="#bbb" font-size="12">4. What we can do</text>
<text x="380" y="302" text-anchor="middle" fill="#eee" font-size="13.5">We can reduce the death toll: give money we spend on things we do not need (e.g. mosquito nets against malaria)</text>
</svg></body></html>
```

The red box is the step that does the work. It is the same view as Bentham's on distance in point 11: if distance and nationality are not morally relevant, the dying children far away count like the child in the street. Singer then says we can act, since each of us spends money on things we do not really need (a new car, a vacation, bottled water where tap water is safe). That money could go to an organisation like the Against Malaria Foundation, which buys bed nets that reliably reduce deaths from malaria, one of the preventable diseases behind the 19,000 deaths a day. The video's tone is distressing, which the lecturer warned about beforehand.

> **Takeaway:** Singer argues that distance, nationality and race make no morally relevant difference, so if we would help a child in front of us, we should help children dying far away when we can.

**Quiz** (`p17_quiz.html`):

```javascript
const Q=[
{p:"Which premise does Singer rely on most to link the child in the street to children far away?",
 o:["Charities are always fully effective","Distance, nationality and race make no morally relevant difference","Everyone must give away all their money"],c:1,
 r:"If distance is not morally relevant, the far-away children count like the child in front of us."},
{p:"What does Singer suggest we give up in order to help?",
 o:["Money spent on things we do not really need","All our savings","Our jobs"],c:0,
 r:"Examples he gives: a new car, a vacation, bottled water when tap water is safe."},
{p:"What does the UNICEF figure in the talk show?",
 o:["About 19,000 children under five die every day of preventable poverty-related diseases","Child deaths are rising every year","Malaria has been eliminated"],c:0,
 r:"6.9 million in 2011, down from 12 million in 1990, but still about 19,000 a day."}
];
```

---

## Point 18. The principle of easy rescue, and the first objections (progress 100%)

Singer's conclusion is his well-known principle of easy rescue: if you can easily rescue someone at modest cost to yourself, you ought to do it. The lecturer then asked the class for objections, and two came up. The first is concentric circles: help the people closest to you first, so with just enough money to help either your mother or someone in Africa, helping your mother makes more sense. The second is effectiveness: Singer's picture seems idealized, assuming a donation is 100% guaranteed to help, and that cannot be definitively proven.

**Visual** (`p18_visual.html`): the principle in a green box, with Objection 1 (concentric circles) and Objection 2 (effectiveness).

```html
<!doctype html><html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<style>body{margin:0;background:#111;color:#eee;font-family:system-ui,sans-serif}svg{width:100%;height:auto;display:block}text{font-family:system-ui,sans-serif}</style></head><body>
<svg viewBox="0 0 760 340" xmlns="http://www.w3.org/2000/svg">
<rect width="760" height="340" fill="#111"/>
<rect x="20" y="15" width="720" height="70" rx="12" fill="#1f7a3d"/>
<text x="380" y="42" text-anchor="middle" fill="#fff" font-size="14" font-weight="700">Principle of easy rescue</text>
<text x="380" y="66" text-anchor="middle" fill="#fff" font-size="14">If you can easily rescue someone with modest cost to yourself, you ought to do it.</text>
<text x="190" y="115" text-anchor="middle" fill="#ff8a80" font-size="14" font-weight="700">Objection 1: concentric circles</text>
<circle cx="190" cy="200" r="78" fill="none" stroke="#888" stroke-dasharray="5 4"/>
<circle cx="190" cy="200" r="50" fill="none" stroke="#888" stroke-dasharray="5 4"/>
<circle cx="190" cy="200" r="22" fill="#3a6ea5"/>
<text x="190" y="205" text-anchor="middle" fill="#fff" font-size="12" font-weight="700">me</text>
<text x="190" y="162" text-anchor="middle" fill="#eee" font-size="11">family</text>
<text x="190" y="132" text-anchor="middle" fill="#eee" font-size="11">strangers far away</text>
<text x="190" y="305" text-anchor="middle" fill="#eee" font-size="12.5">help those closest first, e.g. my mom</text>
<text x="570" y="115" text-anchor="middle" fill="#ff8a80" font-size="14" font-weight="700">Objection 2: effectiveness</text>
<rect x="480" y="150" width="180" height="40" rx="8" fill="#222" stroke="#888"/>
<text x="570" y="175" text-anchor="middle" fill="#eee" font-size="13">my donation</text>
<text x="570" y="222" text-anchor="middle" fill="#eee" font-size="20">?</text>
<rect x="480" y="240" width="180" height="40" rx="8" fill="#222" stroke="#888"/>
<text x="570" y="265" text-anchor="middle" fill="#eee" font-size="13">child actually helped</text>
<text x="570" y="305" text-anchor="middle" fill="#eee" font-size="12.5">Singer assumes 100% effective, not provable</text>
</svg></body></html>
```

The first objection challenges Singer's key premise from point 17, that distance is morally irrelevant. The lecturer called the mother example a tough test case and noted that the mother would have to be as needy as the child, but the rest of the discussion is inaudible in the transcript, so how it ended is unknown. Everything else in the recording, apart from the unrecorded discussion, is covered.

> **Takeaway:** Singer's principle of easy rescue says to help whenever you can at modest cost, and the first objections are that the people closest to us come first and that donations may not be fully effective.

**Quiz** (`p18_quiz.html`):

```javascript
const Q=[
{p:"What does the principle of easy rescue say?",
 o:["Give away everything you own","Only help people you know","If you can easily rescue someone with modest cost to yourself, you ought to"],c:2,
 r:"The key conditions are easy rescue and modest cost."},
{p:"Which Singer premise does the concentric circles objection attack?",
 o:["That distance makes no morally relevant difference","That children die of preventable diseases","That malaria nets exist"],c:0,
 r:"The objection says closeness does matter: help family first."},
{p:"What is the effectiveness objection?",
 o:["Donations are always wasted","Singer idealizes charity, since it is not provable that a donation definitely helps","Charity is forbidden"],c:1,
 r:"The objection is that Singer assumes 100% effectiveness, which cannot be guaranteed."}
];
```

That is the whole lecture. The recording ends in an inaudible discussion, so there is no further point.

---

## Session notes

### Controls used during the session

`.` next point, `,` re-explain the current point, `!` save an item for the summary (a question interrupts the sequence and is answered without a numbered heading).

### Notes saved with `!` (`lecture5_notes.md`, committed and pushed to branch `claude/clever-noether-ix1e7o`)

```markdown
# Lecture 5 notes saved with `!` (for the summary)

- Point 1 (student's wording): "If the large gain outweighs the small losses, the action is right."
  Belongs with: an action usually gives pleasure to some people and pain to others; the theory weighs the balance (pleasures minus pains, summed over everyone affected). Lecture example: refugee shelters in school sports halls, 100 to 200 refugees gain a lot (protection, a bed), many children lose a little (their sports hall). Course phrase: "the greatest good for the greatest number" (Mill).
```

### Quick overview of the lecture in one table

| Point | Topic | Key idea |
|---|---|---|
| 1 | What we look at | Right or wrong depends on the balance of pleasure and pain an action leads to |
| 2 | Maximize | Whatever the good is called, maximize it, summed over everyone |
| 3 | Calculation | Per option: intrinsic goods minus intrinsic bads, choose the best balance |
| 4 | Hedonism vs utilitarianism | One-person calculation versus everyone affected |
| 5 | Bentham's convictions | Equality, ultimate good, calculable |
| 6 | Asceticism | Indirect proof by elimination; asceticism hides a utility principle |
| 7 | Sympathy | No principle, no accountability |
| 8 | Too broad | Malicious pleasures; higher versus lower pleasures (Mill) |
| 9 | Too narrow | Hard worthwhile projects (Rawls example) |
| 10 | Measuring | Intensity, duration, certainty |
| 11 | Remoteness | Distance in space and time; discounting the future |
| 12 | Comparing people | Same number, different meaning; adaptive preferences |
| 13 | Mill and women | Compare the consequences of two options |
| 14 | Three arguments | Men, society, women all worse off |
| 15 | Mill's proof and Moore | Two meanings of "desirable" |
| 16 | Subjective versus objective | Ongoing debate in welfare economics |
| 17 | Singer | Distance is not morally relevant; 19,000 child deaths a day |
| 18 | Easy rescue | Principle and first objections (closeness, effectiveness) |
