import React, { useMemo, useState } from "react";
import { motion } from "framer-motion";

const nav = [
  ["start", "Start Here"],
  ["background", "Company Background"],
  ["who", "WHO / WHY / COMMIT"],
  ["vision", "Vision"],
  ["habits", "Habits"],
  ["industry", "Industry"],
  ["terms", "Insurance Terms"],
  ["damage", "Storm Damage"],
  ["process", "Claims Process"],
  ["appraisal", "Appraisal"],
  ["sales", "Storm Sales"],
  ["cycle", "Sales Cycle"],
  ["followup", "Follow Up"],
  ["guidelines", "Cold Calling"],
  ["pitch", "Open Self Inspection"],
];

const terms = [
  ["Insurer", "Insurance Company providing insurance for the insured"],
  ["Insured", "The individual or business who has insurance"],
  ["Policy Holder", "Individual or business that has ownership of the insurance policy"],
  ["Premium", "The cost of insurance the policy holder pays to keep insurance effective. Usually paid on a per month basis."],
  ["Insurance Policy", "The insurance policy is a contract between the insurer and the insured, known as the policyholder, which determines the claims which the insurer is legally required to pay. In exchange for an initial payment, known as the premium, the insurer promises to pay for loss caused by perils covered under the policy language."],
  ["Deductible", "In the event of an insurance claim, most policies require the insured to pay a deductible AKA Co-Pay on a per claim basis. For example, if an insured has a $10,000 claim with a $1,000 deductible, the insurance company will only pay $9,000 and the insured pays the other $1,000."],
  ["Loss Peril", "A peril is used to describe a specific risk that is covered under the terms of the insurance policy. For example, most policies will have loss peril coverage for hail, wind, fire, water, vandalism, and theft"],
  ["Scope of work", "The work that is to be carried out under a contract to complete a project, broken into deadlines and specific tasks."],
  ["Depreciation", "Decrease in value due to wear and tear, age, decline in price, decay, etc."],
  ["Dwelling", "Livable space. House, apartment, garage, etc."],
  ["Detached Dwelling", "Detached garage, guest house, etc."],
  ["Benefit", "Insurance benefits are the payments your insurance provider guarantees to make after covered services under an insurance policy."],
  ["Exclusion", "A loss risk that is not covered under an insurance policy"],
  ["Recoverable Depreciation", "This is a term that most claims will have which allows the insured to recover the depreciation that insurance withholds on a claim."],
  ["Non-recoverable Depreciation", "This is a term that on rare occasion’s claims will have. This prevents the insured from receiving the depreciation check because the insurance determined that certain/all items on the claim had non-recoverable depreciation."],
];

const claimSteps = [
  ["1", "Meet", "This is the first step in our claims process in which a certified Equity Adjusters representative will meet with the property owner, review the insurance policy and get all the paperwork filled out and signed by the policy holder. The info is then sent to the main Equity Adjusters office and is plugged into our database."],
  ["2", "Initial Prequalifying Inspection", "An Equity Adjusters certified inspector will inspect the property and begin documenting all the damage and create a forensic report showing all the evidence of damage. This report is then sent to our head public adjuster and is reviewed to ensure we do want to file a claim."],
  ["3", "File Claim / Schedule Insurance Inspection", "Equity Adjusters claim processor will then file the claim and insurance will assign an adjuster on that file and schedule a time to meet with Equity Adjusters public adjuster."],
  ["4", "Insurance Inspection", "This is when Equity Adjusters licensed public adjuster will meet with the insurance company on the property and begin negotiating the claim in favor of the insured. The insurance adjuster will either agree or disagree with our report and evidence."],
  ["5", "Negotiations / Estimate Review", "After the first insurance inspection, the insurance company’s adjuster will send in an estimate showing what they are willing to pay. An Equity Adjusters public adjuster will review the estimate to ensure that everything in the claim is being honored."],
  ["6", "Meet with Policy Holder", "After there is an agreement between both adjusters, insurance will send to our office the first ACV check. Our office then will schedule a time where the policy holder and our public adjuster can meet and discuss moving forward."],
  ["7", "Construction", "Equity Adjusters contractor completes the construction work."],
  ["8", "Final Invoicing / Close File", "After we complete the construction work, we then invoice insurance showing that all the work has been completed and they will send the second portion of the claim (RCV). After we receive the RCV and it has been signed by the policy holder, the claim then gets closed out."],
];

const salesCycle = [
  ["Pre-opener", "Before you even go out to sell it is important to make sure you are prepared both physically and mentally."],
  ["Intro / Greeting", "This is your make or break point in the sales cycle. You have 20 seconds or less to make a good first impression."],
  ["Fact Finding / Qualifying", "Ask QUALITY questions and LISTEN. People buy or sign up because they want to solve a problem."],
  ["Inspection", "People believe what they see not what they hear. After completion of inspection you will now have photos to show the homeowner."],
  ["Presentation", "This is where you build value in the service we provide. Know the customer’s dominant buying motive AKA their hot button."],
  ["Close", "The close is the point in the sales process where the homeowners exchange something they value for our service."],
  ["Referral", "The number one best tip on getting referrals is to simply ASK!"],
];

const damageCards = [
  ["Hail Damage", "Hail damage claims are our bread and butter. Hail can damage roofing, soft metals, siding, paint, Air Conditioning Units, storage sheds, windows, window screens, gutters, solar panels, stucco, personal property, etc."],
  ["Spotting Hail Damage", "When prospecting a neighborhood, it is important to know and understand which direction specific storms come from and hit."],
  ["Test Square", "Test squares are used to determine if a roofing system deserves to be replace due to hail damage. To qualify for a roof replacement, typically you need 5+ hail strikes in a 10 ft x 10 ft square area on each slope for insurance to approve."],
  ["Soft Metals / Gutters", "Soft metals are the most susceptible to hail damage and get dented frequently. Gutters are valuable and often times get dented from hail storms."],
  ["Air Conditioning Units", "Notice what hail does to the exposed coils. Insurance will recommend to comb the coils, but if they are torn beyond repair insurance will pay for replacement of the coils. (Big $)"],
  ["Siding / Windows / Paint", "With vinyl siding, damaging hail will break the siding and create holes and chips. Window screens can be dented or torn. Paint chipping is common, especially on the most exposed elevation of the property."],
  ["Wind Damage", "With most violent storms, damaging wind is always a factor. Most roofing systems are wind resistant up to 60 mph. Anything above 60 mph, especially older roofs, have a good chance of receiving wind damage."],
  ["Interior Damage", "Roof leaks are very common, especially with older roofs. The purpose of insurance coverage is to restore your property after a tragic loss, meaning it has to be sudden."],
];

function Badge({ children }) {
  return <span className="rounded-full border border-cyan-300/40 bg-cyan-300/10 px-3 py-1 text-xs font-black uppercase tracking-wide text-cyan-100">{children}</span>;
}

function Section({ id, kicker, title, children }) {
  return (
    <section id={id} className="scroll-mt-24 py-14">
      <motion.div initial={{ opacity: 0, y: 18 }} whileInView={{ opacity: 1, y: 0 }} viewport={{ once: true, margin: "-80px" }} transition={{ duration: 0.45 }}>
        <div className="mb-7">
          <p className="mb-2 text-sm font-black uppercase tracking-[0.25em] text-cyan-600">{kicker}</p>
          <h2 className="max-w-4xl text-4xl font-black tracking-tight text-slate-950 md:text-5xl">{title}</h2>
        </div>
        {children}
      </motion.div>
    </section>
  );
}

function Card({ children, className = "" }) {
  return <div className={`rounded-[2rem] border border-slate-200 bg-white p-6 shadow-sm ${className}`}>{children}</div>;
}

function CheckLine({ children }) {
  return <div className="flex gap-3 rounded-2xl bg-slate-50 p-4 text-sm font-bold leading-6 text-slate-700"><span className="flex h-6 w-6 shrink-0 items-center justify-center rounded-full bg-cyan-500 text-white">✓</span>{children}</div>;
}

function VisualRoof() {
  return (
    <div className="relative h-72 overflow-hidden rounded-[2rem] bg-gradient-to-br from-slate-900 via-slate-800 to-cyan-900 p-6 text-white shadow-xl">
      <div className="absolute inset-0 opacity-30">
        <div className="absolute left-8 top-8 h-24 w-24 rounded-full bg-cyan-300 blur-3xl" />
        <div className="absolute bottom-8 right-8 h-32 w-32 rounded-full bg-blue-500 blur-3xl" />
      </div>
      <div className="relative z-10">
        <p className="text-sm font-black uppercase tracking-[0.25em] text-cyan-200">Training Visual</p>
        <h3 className="mt-2 text-3xl font-black">From Door Knock to Claim Victory</h3>
      </div>
      <div className="absolute bottom-10 left-8 right-8 h-20 rounded-xl bg-slate-700 shadow-2xl [clip-path:polygon(0_45%,50%_0,100%_45%,100%_100%,0_100%)]" />
      {[20, 70, 120, 170, 220, 270, 320, 370, 420].map((x) => <div key={x} className="absolute bottom-12 h-14 w-12 rotate-45 rounded-md border-2 border-cyan-200/40" style={{ left: x }} />)}
      {[1,2,3,4,5,6,7].map((n) => <div key={n} className="absolute top-20 h-3 w-3 rounded-full bg-cyan-300 shadow-[0_0_20px_#67e8f9]" style={{ left: `${12 + n*11}%`, top: `${60 + (n%3)*18}px` }} />)}
    </div>
  );
}

function LightningVisual() {
  return <div className="mx-auto my-6 flex h-28 w-28 items-center justify-center rounded-[2rem] bg-gradient-to-br from-yellow-300 to-cyan-500 text-6xl shadow-xl">⚡</div>;
}

function PhoneMock({ children }) {
  return <div className="mx-auto max-w-sm rounded-[2.5rem] border-8 border-slate-900 bg-slate-950 p-3 shadow-2xl"><div className="rounded-[2rem] bg-white p-5 text-slate-900">{children}</div></div>;
}

export default function EquityAdjustersHandbookWebsite() {
  const [query, setQuery] = useState("");
  const filtered = useMemo(() => nav.filter(([, label]) => label.toLowerCase().includes(query.toLowerCase())), [query]);

  return (
    <div className="min-h-screen bg-slate-50 text-slate-900">
      <header className="sticky top-0 z-50 border-b border-slate-200 bg-white/90 backdrop-blur-xl">
        <div className="mx-auto flex max-w-7xl items-center justify-between gap-4 px-5 py-4">
          <a href="#start" className="flex items-center gap-3">
            <div className="flex h-12 w-12 items-center justify-center rounded-2xl bg-gradient-to-br from-slate-950 to-cyan-700 text-sm font-black text-white shadow-lg">EA</div>
            <div>
              <div className="text-sm font-black uppercase tracking-wider text-slate-950">Equity Adjusters</div>
              <div className="text-xs font-bold text-slate-500">Employee Handbook 2026</div>
            </div>
          </a>
          <nav className="hidden gap-2 xl:flex">
            {nav.slice(0, 8).map(([id, label]) => <a className="rounded-full px-3 py-2 text-xs font-black text-slate-600 hover:bg-slate-100 hover:text-slate-950" href={`#${id}`} key={id}>{label}</a>)}
          </nav>
        </div>
      </header>

      <main id="start" className="mx-auto max-w-7xl px-5">
        <section className="grid min-h-[84vh] items-center gap-10 py-16 lg:grid-cols-[1.05fr_.95fr]">
          <motion.div initial={{ opacity: 0, y: 24 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: .55 }}>
            <div className="mb-5 flex flex-wrap gap-2"><Badge>Fairness</Badge><Badge>Balance</Badge><Badge>Advocacy</Badge><Badge>Storm Restoration</Badge></div>
            <h1 className="text-5xl font-black leading-[.95] tracking-tight text-slate-950 md:text-7xl">The Equity Adjusters Playbook</h1>
            <p className="mt-6 max-w-3xl text-xl font-semibold leading-9 text-slate-700">A high-energy website version of the employee handbook — built to train new reps, teach the claims process, build belief, sharpen sales skills, and get the team excited to serve property owners.</p>
            <div className="mt-8 flex flex-col gap-3 sm:flex-row"><a href="#who" className="rounded-2xl bg-slate-950 px-6 py-4 text-center text-sm font-black text-white shadow-lg hover:bg-cyan-800">Start Training →</a><a href="#pitch" className="rounded-2xl border border-slate-300 bg-white px-6 py-4 text-center text-sm font-black text-slate-950 shadow-sm hover:bg-slate-100">Jump to Pitch</a></div>
          </motion.div>
          <motion.div initial={{ opacity: 0, scale: .96 }} animate={{ opacity: 1, scale: 1 }} transition={{ duration: .55, delay: .1 }}><VisualRoof /></motion.div>
        </section>

        <section className="rounded-[2rem] border border-slate-200 bg-white p-5 shadow-sm md:p-7">
          <div className="mb-4 flex flex-col gap-3 md:flex-row md:items-end md:justify-between">
            <div><h2 className="text-2xl font-black">Training Map</h2><p className="text-sm font-semibold text-slate-500">Move through the handbook in the right order, or search for the exact section you need.</p></div>
            <input value={query} onChange={(e) => setQuery(e.target.value)} placeholder="Search the handbook..." className="w-full rounded-2xl border border-slate-200 bg-slate-50 px-4 py-3 text-sm font-semibold outline-none focus:border-cyan-500 md:w-80" />
          </div>
          <div className="grid gap-3 sm:grid-cols-2 lg:grid-cols-4">
            {filtered.map(([id, label], i) => <a key={id} href={`#${id}`} className="group rounded-2xl border border-slate-200 bg-slate-50 p-4 transition hover:-translate-y-0.5 hover:border-cyan-300 hover:bg-cyan-50 hover:shadow-md"><div className="mb-2 text-xs font-black text-cyan-700">{String(i + 1).padStart(2, "0")}</div><div className="font-black text-slate-950">{label}</div></a>)}
          </div>
        </section>

        <Section id="background" kicker="Foundation" title="Company Background">
          <div className="grid gap-6 lg:grid-cols-3">
            <Card className="lg:col-span-2"><p className="text-lg leading-9 text-slate-700">Equity Adjusters stands for fairness and Balance. The company was founded in 2020 and has recovered thousands of dollars for our clients. We are an advocacy group that provides services and products that further protect, repair, and add value to the property owner’s investment. The focus for this manual is our insurance claim representation service, in which we represent property owners with their insurance claims to maximize their settlements.</p><p className="mt-5 text-lg leading-9 text-slate-700">We handle claims such as wind, hail, fire, flood, and vandalism. Essentially, any claim a property owner might have, we handle it. The focus for this manual, are residential and commercial roofing claims for losses occurred by wind and hail damage.</p></Card>
            <Card className="bg-slate-950 text-white"><LightningVisual /><h3 className="text-2xl font-black">Your Mission</h3><p className="mt-3 leading-7 text-slate-300">Protect the property owner. Understand the claim. Document the damage. Maximize the settlement. Represent the brand.</p></Card>
          </div>
        </Section>

        <Section id="who" kicker="Identity" title="WHO are you? I AM.">
          <div className="grid gap-6 lg:grid-cols-2">
            <Card><h3 className="mb-3 text-2xl font-black">It starts with who you are.</h3><p className="leading-8 text-slate-700">It is important that you know who you are. You are more than the name that was given to you. We want to know what it is that makes you, you! There is much power behind the I am statement. Think of the three best attributes that best describe who you are.</p><div className="mt-5 grid gap-3"><CheckLine>Write down the top 3 attributes that describe who you are.</CheckLine><CheckLine>Write down 3 things that motivate you.</CheckLine><CheckLine>Write down 3 reasons why you are here.</CheckLine><CheckLine>Write down 3 things you will bring to the table and commit to.</CheckLine></div></Card>
            <Card className="bg-gradient-to-br from-cyan-700 to-slate-950 text-white"><p className="text-sm font-black uppercase tracking-[0.25em] text-cyan-200">Understanding The WHY Factor</p><h3 className="mt-3 text-3xl font-black">GO ALL IN</h3><blockquote className="mt-5 rounded-2xl bg-white/10 p-5 text-xl font-black leading-9">“Whatever you want, go ALL IN and DOMINATE, learn it, eat it, sleep it, breathe it and believe it”<br/><span className="text-sm text-cyan-200">- Grant Cardone</span></blockquote><p className="mt-5 leading-8 text-cyan-50">Why are you here? Is it money? Is it a fresh start? Does the idea of being your own boss motivate you? Maybe you have dreams of traveling the world. Bottom line, you need to understand your WHY.</p></Card>
          </div>
          <div className="mt-6 grid gap-4 md:grid-cols-4">{[["WHO", "Who are you?"],["WHY", "Why are you here?"],["COMMIT", "What do you commit to?"],["STATEMENT", "Combine it into action."]].map(([a,b],i)=><div className="rounded-[2rem] bg-white p-6 shadow-sm ring-1 ring-slate-200" key={a}><div className="mb-4 flex h-12 w-12 items-center justify-center rounded-2xl bg-slate-950 text-lg font-black text-white">{i+1}</div><h4 className="font-black">{a}</h4><p className="mt-1 text-sm font-semibold text-slate-600">{b}</p></div>)}</div>
        </Section>

        <Section id="vision" kicker="Target" title="Vision Statement Checklist">
          <Card><p className="text-lg leading-9 text-slate-700">A checklist that helps you keep focused on what you want in your life. You need to understand your WHY. Here you will create a vision statement. A vision statement should be a paragraph or two that describes your targets in your personal life, business/company, and financial situation over the next year. It is something that you can read daily to remind yourself what you are going to accomplish over the next twelve months. Think BIG! If your goals don’t motivate you than they are not big enough.</p><div className="mt-6 grid gap-4 md:grid-cols-3"><Card className="bg-cyan-50"><h3 className="font-black">Personal</h3><p className="mt-2 text-sm leading-6 text-slate-700">How do you want your life to look? How do you want your health to be? What places do you want to go? Where will you live? What will you drive? How will others see you?</p></Card><Card className="bg-cyan-50"><h3 className="font-black">Business / Company</h3><p className="mt-2 text-sm leading-6 text-slate-700">What will your position be? How will you grow Equity Adjusters? What market will you be working? Who will be on your team?</p></Card><Card className="bg-cyan-50"><h3 className="font-black">Financial</h3><p className="mt-2 text-sm leading-6 text-slate-700">How much will you earn? Do you want to be debt free? Will you have residual income? What will you do with the money you want to earn?</p></Card></div></Card>
        </Section>

        <Section id="habits" kicker="Discipline" title="Develop Habits">
          <div className="grid gap-6 lg:grid-cols-[.9fr_1.1fr]"><Card><p className="text-lg leading-9 text-slate-700">Developing habits are what shape the kind of life you want. It is important to focus on the end result and what you want in the long term, but it is what you do every SINGLE day that matters more than anything. Focusing on your everyday habits will ensure you are on the right path to get the end result.</p></Card><Card><div className="grid gap-3 sm:grid-cols-2"><CheckLine>Wake up before 7 A.M</CheckLine><CheckLine>Read at least 20-30 mins</CheckLine><CheckLine>Workout and eat as clean as possible</CheckLine><CheckLine>No matter how busy I am always make time for my family/loved ones</CheckLine><CheckLine>Continue to grow Equity Adjusters by making sure I am producing business everyday</CheckLine><CheckLine>Review what is left unchecked before sleep</CheckLine></div></Card></div>
        </Section>

        <Section id="industry" kicker="Opportunity" title="How Big Is The Industry? We Are In A Recession Proof Industry">
          <Card><p className="text-lg leading-9 text-slate-700">In 2014, there were a total of $110 billion of global catastrophic losses, with the ten-year average right around $190 billion. There were a total of 980 loss events in 2014, with the ten-year average at 830. In 2014, there were $15.3 billion in losses from thunderstorms just here in the United States. These are the types of storms that produce damaging hail and winds in which we flourish with.</p><p className="mt-5 text-lg leading-9 text-slate-700">No matter what the economy looks like, people will always have to protect their investments with insurance, and catastrophic events are continuing to become more frequent.</p><div className="mt-6 grid gap-4 md:grid-cols-3"><div className="rounded-[2rem] bg-slate-950 p-6 text-white"><div className="text-4xl font-black">$110B</div><p className="mt-2 text-sm text-slate-300">Global catastrophic losses in 2014</p></div><div className="rounded-[2rem] bg-cyan-700 p-6 text-white"><div className="text-4xl font-black">980</div><p className="mt-2 text-sm text-cyan-50">Loss events in one year</p></div><div className="rounded-[2rem] bg-white p-6 ring-1 ring-slate-200"><div className="text-4xl font-black text-slate-950">$15.3B</div><p className="mt-2 text-sm text-slate-600">U.S. thunderstorm losses in 2014</p></div></div></Card>
        </Section>

        <Section id="terms" kicker="Education" title="General Terms & Claim Payments">
          <div className="grid gap-4 md:grid-cols-2">{terms.map(([t,d])=><div key={t} className="rounded-2xl bg-white p-5 shadow-sm ring-1 ring-slate-200"><h3 className="font-black text-slate-950">{t}</h3><p className="mt-2 text-sm leading-6 text-slate-700">{d}</p></div>)}</div>
          <Card className="mt-6 bg-slate-950 text-white"><h3 className="text-2xl font-black">How Is An Insurance Claim Paid Out?</h3><p className="mt-3 leading-8 text-slate-300">When the insured has a loss event the claim is typically broken up into two payments. The first payment is called the Actual Cash Value (ACV) Payment. The second payment is the Replacement Cost Value (RCV) payment. In order to recover the second payment, or the RCV payment, the insured must first replace/fix everything within the insurance scope that was paid.</p></Card>
        </Section>

        <Section id="damage" kicker="Field Knowledge" title="Identifying Storm Damage">
          <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-4">{damageCards.map(([t,d])=><Card key={t}><h3 className="font-black">{t}</h3><p className="mt-2 text-sm leading-6 text-slate-700">{d}</p></Card>)}</div>
        </Section>

        <Section id="process" kicker="Operations" title="The Claims Process">
          <div className="relative grid gap-4 md:grid-cols-2 lg:grid-cols-4">{claimSteps.map(([n,t,d])=><div key={n} className="rounded-[2rem] bg-white p-6 shadow-sm ring-1 ring-slate-200"><div className="mb-4 flex h-12 w-12 items-center justify-center rounded-2xl bg-gradient-to-br from-slate-950 to-cyan-700 text-xl font-black text-white">{n}</div><h3 className="font-black text-slate-950">{t}</h3><p className="mt-2 text-sm leading-6 text-slate-700">{d}</p></div>)}</div>
        </Section>

        <Section id="appraisal" kicker="When Claims Are Underpaid" title="Appraisal Process">
          <div className="grid gap-6 lg:grid-cols-2"><Card><p className="text-lg leading-9 text-slate-700">If our public adjuster and the insurance adjuster cannot come to an agreement on a claim, then we take the claim to appraisal. In all policies, there is a section called the appraisal clause which states, at any given time if the insurer and the insured cannot agree on the amount of loss, either party can initiate appraisal.</p><p className="mt-5 text-lg leading-9 text-slate-700">Essentially it allows the insured and the insurer to hire their own third party independent appraiser and then both appraisers will meet at the property and work together to come into an agreement. This is our bread and butter when claims do not get paid fairly upfront.</p></Card><Card className="bg-cyan-50"><h3 className="text-2xl font-black">Umpire + FAQ</h3><div className="mt-4 grid gap-3"><CheckLine>If appraisers cannot agree, each appraiser will elect to hire an umpire.</CheckLine><CheckLine>The appraiser fee is typically paid out of extra money won on top of the claim.</CheckLine><CheckLine>The cost for an umpire is split between both appraisers working on the file.</CheckLine><CheckLine>Typically, the appraisal process will take anywhere from 30-90 days.</CheckLine><CheckLine>We have about a 90%-win rate when we initiate the appraisal process.</CheckLine></div></Card></div>
        </Section>

        <Section id="sales" kicker="Mindset" title="Storm Restoration Sales">
          <Card><h3 className="text-3xl font-black">You need to be SOLD on selling</h3><p className="mt-4 text-lg leading-9 text-slate-700">The most important sale you will ever make is to yourself. You need to be sold on the idea that selling is your golden ticket to get everything you want in life. The fact is, whether you know it or not, you are always selling. Throughout your life, you will always have to sell, persuade, negotiate, and convince others on your ideas regardless of your position.</p><p className="mt-4 text-lg leading-9 text-slate-700">The reason why we love storm sales is because we bring people MONEY. Everybody loves money! This is literally the easiest sale you can make. We do not charge our clients directly for our services. In fact, they do not pay us a single dime for what we do. The more money we win for the property owner, the more you make. It’s a no brainer!!!!</p><div className="mt-6 grid gap-3 md:grid-cols-3"><CheckLine>Dress professionally</CheckLine><CheckLine>Good hygiene</CheckLine><CheckLine>Walk with a purpose</CheckLine><CheckLine>Avoid distractions</CheckLine><CheckLine>Your voice</CheckLine><CheckLine>Be calm, relaxed, and collected</CheckLine></div></Card>
        </Section>

        <Section id="cycle" kicker="System" title="Sales Cycle">
          <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-4">{salesCycle.map(([t,d],i)=><div key={t} className="rounded-[2rem] bg-white p-6 shadow-sm ring-1 ring-slate-200"><div className="mb-4 text-4xl font-black text-cyan-700">{i+1}</div><h3 className="font-black">{t}</h3><p className="mt-2 text-sm leading-6 text-slate-700">{d}</p></div>)}</div>
          <Card className="mt-6 bg-slate-950 text-white"><h3 className="text-2xl font-black">NUMBER ONE RULE OF SELLING</h3><p className="mt-3 text-lg leading-9 text-slate-300">Always, always, ALWAYS agree with the customer! This is the single most important rule of selling. Any objection or any response a prospect might give you, your first rule is to agree. You cannot sell someone by arguing, being confrontational, or simple disagreeing.</p><div className="mt-5 flex flex-wrap gap-2">{["I understand…","Absolutely!","I get it!","Perfect!","I can handle that for you…","No problem!","Excellent!","Anything for you!"].map(x=><span key={x} className="rounded-full bg-white/10 px-4 py-2 text-sm font-bold">{x}</span>)}</div></Card>
        </Section>

        <Section id="followup" kicker="Conversion" title="Follow Up">
          <Card><p className="text-lg leading-9 text-slate-700">The biggest difference between a sales professional and an amateur is the amount of effort used in the follow up. Follow up is the single most important skill you must develop that will ultimately determine your level of success in this business. Every prospect you talk to you is like a seed, you need to nurture the seed, water it, give it sunlight, and with proper care the seed will grow.</p><div className="mt-6 grid gap-4 md:grid-cols-4"><div className="rounded-[2rem] bg-slate-950 p-6 text-white"><div className="text-3xl font-black">48%</div><p className="mt-2 text-sm">of sales people never follow up</p></div><div className="rounded-[2rem] bg-cyan-700 p-6 text-white"><div className="text-3xl font-black">25%</div><p className="mt-2 text-sm">never make a second contact</p></div><div className="rounded-[2rem] bg-white p-6 ring-1 ring-slate-200"><div className="text-3xl font-black">&lt;10%</div><p className="mt-2 text-sm text-slate-600">of sales are made on first contact</p></div><div className="rounded-[2rem] bg-white p-6 ring-1 ring-slate-200"><div className="text-3xl font-black">70%+</div><p className="mt-2 text-sm text-slate-600">of sales are made between 5th-12th contact</p></div></div><div className="mt-6 grid gap-3 sm:grid-cols-2 lg:grid-cols-3">{["Text messaging","Personal Visits","Phone calls","Skype call","Email","Written letters"].map(x=><CheckLine key={x}>{x}</CheckLine>)}</div></Card>
        </Section>

        <Section id="guidelines" kicker="Standards" title="Cold Calling Guidelines">
          <div className="grid gap-4 md:grid-cols-2 lg:grid-cols-3">{[
            ["Be honest, transparent, and straight forward", "People will know if you are lying. DO NOT EVER lie to the customer to get the sale."],
            ["Be interesting — then be interested", "First you must be interesting so that you grab the prospects attention. Then you need to be interested in them."],
            ["Believe you can make a sale on every call", "Before ever calling on a prospect you must believe in your mind that you will make the sale no matter what."],
            ["Identify & solve problems", "This is what professional salespeople do! You are there to solve a problem."],
            ["Be logical & structured", "Do not just wing it. Walk the homeowner through a process step by step."],
            ["Be respectful", "Remember you are a professional. You absolutely cannot be rude, or offensive."],
            ["Be enthusiastic, be positive", "You need to be excited about your job!"],
            ["Be memorable", "Be different. This is where your personality comes in and you leave a mark."],
            ["Always smile", "Smiling can drop their guard and lighten the mood."],
          ].map(([t,d])=><Card key={t}><h3 className="font-black">{t}</h3><p className="mt-2 text-sm leading-6 text-slate-700">{d}</p></Card>)}</div>
        </Section>

        <Section id="pitch" kicker="Door Script" title="Open Self Inspection Pitch">
          <div className="grid gap-6 lg:grid-cols-[1.05fr_.95fr]"><Card><div className="space-y-4 text-lg leading-9 text-slate-700"><p>Hello, glad to catch you at home. My name is <b>(__________)</b>. I work for a public adjusting firm named Equity Adjusters. I take it you’re the homeowner here?</p><p>Fantastic. We are property claims adjusters. We’re local and licensed in the greater Salt Lake area. We’re in your neighborhood today helping homeowners get their roofs paid for and replaced through homeowners insurance.</p><p>We carry the same license as the insurance companies, and we are licensed with the Department of Insurance in the State of Utah. What we do is perform inspections to determine whether there is enough storm-related damage for the insurance company to pay for a full roof replacement.</p><p>Again, my name is <b>(__________)</b>. What was your name?</p><p>Pleasure to meet you, <b>(__________)</b>.</p><p>How long have you owned the home?</p><p>How old is the roof?</p><p>Have you had any repairs done to the roof before?</p><p>Have you experienced any interior leaking?</p><p>Perfect. What I’m going to do now is complete a quick inspection of the roof to see whether the property qualifies for the insurance company to pay for a full replacement.</p><p>While I’m doing the inspection, do me a favor and locate your insurance information. The inspection should only take a few minutes, and I’ll come back down and review everything with you once I’m finished.</p><p>Pleasure meeting you, and I’ll be back down shortly.</p></div></Card><div><PhoneMock><div className="mb-4 rounded-2xl bg-cyan-50 p-4 text-center text-sm font-black text-cyan-800">FIELD REP MODE</div><div className="space-y-3"><CheckLine>Confident</CheckLine><CheckLine>Licensed</CheckLine><CheckLine>Professional</CheckLine><CheckLine>Helpful</CheckLine><CheckLine>Calm</CheckLine><CheckLine>Assumptive, not pushy</CheckLine></div></PhoneMock></div></div>
        </Section>

        <footer className="border-t border-slate-200 py-12 text-center"><h2 className="text-3xl font-black">Equity Adjusters Standard</h2><p className="mx-auto mt-4 max-w-3xl text-lg leading-8 text-slate-600">Know who you are. Know why you are here. Commit fully. Learn the industry. Serve property owners. Follow the process. Stay positive. Follow up. Always smile.</p></footer>
      </main>
    </div>
  );
}
