# Annotation Guidelines: Frame-Semantic Annotation of EU Reporting Requirements

**Tool:** INCEpTION, three custom span layers (`LU`, `Frame`, `FE`)
**Unit of annotation:** one *reporting request* (a single legislative provision)

---

## 1. Basic FrameNet vocabulary

This section defines the core terms used throughout this document, for anyone not already familiar with linguistics, Frame Semantics or FrameNet.

- **Frame.** A structured description of a recurring type of situation, along with the participants and circumstances relevant to it. For example, the frame `Telling` describes any situation where someone communicates something to someone else.
- **Lexical Unit (LU).** The specific word (or fixed multiword expression) in the text that signals, or *evokes*, a frame. In "ESMA shall **submit** the standards...", the verb *submit* is the LU that evokes `Telling`.
- **Role.** One of the participant or circumstance slots that a frame defines, independently of any particular sentence. `Telling` defines the roles Speaker, Addressee, Message, Medium, and Topic; any sentence that evokes `Telling` may fill some subset of these.
- **Argument / Frame Element (FE).** FrameNet's term for a role once it has been filled by an actual span of text in a specific sentence. This document uses "argument" and "Frame Element" interchangeably to mean this filled slot (e.g. "the Message FE of this Telling instance").
- **Filler.** The actual span of text occupying a role. In "ESMA shall submit the standards to the Commission", *ESMA* is the filler of the Speaker role, and *the Commission* is the filler of the Addressee role.
- **Conjunct.** One item in a coordinated list joined by "and"/"or"/commas. In "the Parliament, the Council and the Commission", there are three conjuncts.
- **Modal.** An auxiliary verb expressing obligation, permission, or possibility. In this corpus the modal is almost always *shall* (obligation) or *may* (permission). Modals are never included in FE spans (§4.6).

---

## 2. What you are annotating

A *reporting request* is a legislative provision in which an **Addresser** (a Member State, agency, or EU body) must supply an **Artifact** (a report, technical standard, survey, opinion, notification, etc.) to an **Addressee** (typically the Commission, Council, Parliament, or another EU body), optionally under a **Condition**, within a **Time** constraint, and possibly at a certain **Frequency**.

Six FrameNet frames make this structure explicit:

| Frame | Captures |
|---|---|
| `Telling` | The reporting act itself: who tells what to whom |
| `Intentionally_create` | The prior act of producing the artifact, when the text says it must be developed/drafted/created |
| `Conditional_scenario` | The condition(s) under which the request applies |
| `Time_vector` | The deadline / temporal constraint |
| `Frequency` | How often the request recurs |
| `Artifact` | The reported object itself, and its internal part-whole structure |

**Main frames**

**Scope boundary: creation and transmission of RR only.** We annotate exactly two kinds of event: the *creation* of a reportable artifact (`Intentionally_create`) and its *transmission* from the Addresser to the Addressee (`Telling`). We do not annotate what happens to the artifact afterwards: its formal adoption, approval, or entry into force by the recipient is out of scope. For example, in "*Power is delegated to the Commission to adopt the regulatory technical standards referred to in the first subparagraph in accordance with Articles 10 to 14 of Regulation (EU) No 1095/2010*," no frame from our frame corpus is evoked: *adopt* describes the Commission's own action on a submitted artifact, not its creation or transmission, so it falls outside our scope.

**Passive voice**

Both the Speaker and the Addressee can be **implicit** (left unmentioned in the sentence) as long as the creation or transmission event itself is present. In "*The report shall be published*," `Telling` is evoked by the LU `publish.v` with only a `Message` FE (the report); there is no explicit Speaker or Addressee in the sentence, and none should be added or inferred. The same principle applies to `Intentionally_create`'s `Creator`: when a passive construction gives no explicit agent (e.g. "*financial reports shall be prepared in a single electronic reporting format*"), tag `Created_entity` alone and leave `Creator` unlinked rather than guessing.

**Supporting frames**

**The four supporting frames are never annotated on their own.** `Time_vector`, `Frequency`, `Artifact`, and `Conditional_scenario` exist only to characterize a `Telling` or `Intentionally_create` instance — a deadline, a recurrence rate, a described artifact, or a condition is only relevant to this scheme if it attaches to a reporting or artifact-creation event that is itself annotated. If an LU for one of these four frames instead attaches to some other kind of action that falls outside our scope (e.g. a deadline on the Commission's *adoption* of a standard, rather than on its submission), do not annotate it, even though the same LU would be annotated if it modified a `Telling` or `Intentionally_create` instance elsewhere in the corpus.

---

## 3. The three INCEpTION layers

Every frame annotation involves three coordinated layers, always applied **in this order**:

1. **LU (Lexical Unit)** — mark the word(s) that evoke the frame and tag it with `lemma.POS`. The **lemma** is the dictionary base form of the word (e.g. *develop*, not *developed*/*develops*). The **POS** is an abbreviated part-of-speech code appended after a period, following FrameNet's own convention:

   | Code | Part of speech | Example |
   |---|---|---|
   | `.v` | verb | `develop.v`, `submit.v` |
   | `.a` | adjective | `quarterly.a` |
   | `.adv` | adverb | `annually.adv` |
   | `.prep` | preposition | `by.prep`, `after.prep` |
   | `.conj` | coordinating conjunction | `if.conj` |

   For a multiword expression that functions as a single unit (a complex preposition, a support-verb + noun construction, or a subordinating connective made of several words), tag every token of the expression with the *same* LU value, joining the words of the lemma with underscores (e.g. `as_part_of.prep`, `not_later_than.conj`).
2. **Frame** — mark the *same span* as the LU and assign the frame name (`Telling`, `Time_vector`, etc.). The LU and Frame spans always cover exactly the same words.
3. **FE (Frame Element)** — mark each argument's span, then, from the Frame annotation, link that span to the appropriate role (Speaker, Addressee, Event, etc.) using the role list defined for that frame.

Practical rule for FE spans: always create an FE annotation over an argument, even if it is a single word (e.g. "EBA", "it"). Then link it to a role via the Frame annotation's slot filler.

---

## 4. General annotation principles

**4.1 Scope.** Annotate within a single provision. A Frame Element may occasionally reach into a previous sentence of the *same* provision (e.g. an Addressee introduced earlier and referred to anaphorically later).

**4.2 Spans must be contiguous, but can be nested.** An FE span cannot skip words. However, one FE span can sit entirely inside another (e.g. the whole clause "submit the draft technical standards ... to the Commission" is the `Event` of `Time_vector`, and it contains, nested inside it, the `Message` and `Addressee` spans of the `Telling` frame that also occupies that clause).

**4.3 One span can fill roles in more than one frame.** Do not duplicate an FE span if the same stretch of text is genuinely the correct filler for two different frames' roles.

**Worked example** (same real sentence, annotated twice, once per `Time_vector` instance):
> *Based on that report and __after__ [Direction] __consulting the ECB__ [Landmark_event], the Commission shall, by 2014-12-31, __submit a report to the European Parliament and to the Council__ [Event] on the use of and benefits from those refinancing operations...* (LU: `after.prep`)
> *Based on that report and after consulting the ECB, the Commission shall, __by__ [Direction] __2014-12-31__ [Landmark_event], __submit a report to the European Parliament and to the Council__ [Event] on the use of and benefits from those refinancing operations...* (LU: `by.prep`)

Here the same clause, "submit a report to the European Parliament and to the Council," is the `Event` FE of *two separate* `Time_vector` instances: one anchored to "consulting the ECB," the other to "2014-12-31." Both instances link to the exact same FE span; it is created once and reused, not duplicated. The same principle applies across different frames, not just two instances of the same one: e.g. a Message of `Telling` that is also the Artifact of an `Artifact` frame should likewise be linked from both rather than re-tagged twice.

**4.4 Several frames per provision are normal; the same frame can recur.** Most provisions evoke 2–4 of the six frames. It is also normal for the same frame to be evoked twice in one provision (e.g. two separate `Telling` events, or `Time_vector` evoked by two different deadline expressions, as in the example above).

**4.5 Repeated roles for coordinated fillers.** When a role has multiple distinct fillers joined by "and"/commas (e.g. "the European Parliament, the Council and the Commission"), create **one FE span per conjunct** and link each separately to the same role (three separate `Addressee` links), rather than one span covering the whole coordinated phrase.

**4.6 Event-FE span boundaries.** When an FE (typically `Event` in `Time_vector` or `Frequency`) points to "the action described by the governing clause," start the span at the verb itself and extend it through the end of the relevant clause. Do not include the subject or the modal ("shall"/"may"). **Exception:** when the verb is passive and its grammatical subject is the *patient* of the action rather than an agent (i.e. the thing being acted on, not the one acting, as in "*the report shall be prepared*," where "the report" is what gets prepared, not who prepares it), include the subject and modal in the Event span. This reflects that there is no separate agent to exclude the subject in favour of; the subject **is** the content of the event being time-located. Compare: "*[submit those draft regulatory technical standards to the Commission]* [Event] by 2016-12-31" (active voice, exclude the subject "ESMA") vs. "*[Those reports shall be communicated to the Commission]* [Event]" (passive, no separate agent, include the subject).

**4.7 Prefer the closest mention, not the most explicit one.** When an entity is referred to more than once in the same provision (e.g. once by full name ("EBA") and again later by a pronoun ("it")) and either mention could fill a role of the frame being annotated, tag whichever mention is *syntactically closest* to the frame-evoking word, not necessarily the fuller or more explicit one. Do not default to the full name out of a preference for explicitness. For example, if a provision opens with "the Authority" and later says "..., it shall disclose the results," the Speaker of that `Telling` instance is "it", because "it" is the mention closest to *disclose*, not "the Authority".

**4.8 Coordinated fillers vs. frame duplication.** When a `Telling` (or other) instance would otherwise need more than one filler for the *same* role, decide between §4.5's coordination rule and duplicating the Frame annotation, based on whether each filler needs its own distinct value for some *other* role:
- If the fillers are a simple coordinated list and no other role needs to pair uniquely with just one of them (e.g. "forward the application, the evaluation report and the supporting dossier" has three Messages, no per-item Topic), tag each as a separate link on the role, on the *same* frame instance, following §4.5.
- If each filler has its own distinct value for another role that must stay correctly paired with it (e.g. two Messages, each with its own separate Topic: see §5.1 for a full worked example), simply repeating both roles on one instance would leave it ambiguous which Topic goes with which Message. Duplicate the Frame annotation instead: create two separate instances of the same frame (e.g. two `Telling` frames) on the same LU span, each with its own Message and Topic, while roles that are not ambiguous (e.g. Speaker, Addressee) can be linked identically on both.

**4.9 "In cooperation/collaboration with X" does not make X a co-Speaker/co-Creator.** When a sentence names a primary responsible agent and then adds a prepositional phrase naming other bodies it works with (e.g. "the Commission shall, *in close cooperation with* the Authority and the Member States, draw up..."), tag only the grammatical subject as Speaker/Creator. The "in cooperation with" phrase describes the manner in which the primary agent acts, not a second, coordinated subject; unlike a genuine coordination such as "the Commission and EBA shall submit," which would warrant tagging both. This is different from a body being merely *consulted* (e.g. "after consulting the ECB"), which never warrants a Speaker/Creator link at all.

---

## 5. The six frames

### 5.1 Telling
**Definition.** A Speaker addresses an Addressee with a Message (which may be indirectly referred to as a Topic).

**Frame Elements used:** `Speaker` (repeatable), `Addressee` (repeatable), `Message` (repeatable, see §4.8 for when to repeat vs. duplicate the frame), `Medium` (not yet observed to repeat in the corpus), `Topic` (repeatable, see §4.8).

**`Telling` never takes a `Purpose` FE.** `Purpose` belongs only to `Intentionally_create` (§5.2). `Telling` can take `Topic` instead, which plays a related but distinct role: `Topic` says what an already-existing Message *concerns*, while `Purpose` says why an artifact still to be created is being made. Do not use one where the other belongs, and do not add `Purpose` to a `Telling` instance.

**Careful: do not cross the two frames' analogous roles.** `Telling`'s Speaker and `Intentionally_create`'s Creator (§5.2) look similar, as both name the responsible agent, but they belong to different frames and must never be used on the wrong one.

**Scope note (deliberate broadening):** in this corpus, `Telling` is used for any act of a report/document/opinion being delivered, supplied, or attached to a recipient, and is not only triggered by canonical communication verbs. This includes verbs like *submit, inform, disclose, provide, publish, report, send*, and also verbs like *accompany* when a document is said to accompany or supplement the main report (Message = the accompanying document).

**Message vs. Topic.** Use `Message` for the report/content noun itself (e.g. "a report", "its reasoning"). Use `Topic` for a following "on/about X" phrase that specifies what the report concerns, when Message and Topic are expressed separately (e.g. "send a quarterly **report** [Message] **on progress in the operational implementation of this Regulation** [Topic]").

**Worked example** (from the corpus; **bold** marks the exact span tagged, `[Role]` gives its role):
> *__ESMA__ [Speaker] shall submit __those draft regulatory technical standards__ [Message] to __the Commission__ [Addressee] by 2018-07-21.*
LU: `submit.v`.

**Particular case: two Messages, each with its own Topic.** Consider: *"Based on that report and after consulting the ECB, the Commission shall, by 2014-12-31, submit a report to the European Parliament and to the Council on the use of and benefits from those refinancing operations and funding support measures for credit institutions authorised in the Union, together with a legislative proposal on the use of such refinancing operations and funding support measures if appropriate."* This sentence reports two distinct things ("a report" and "a legislative proposal"), each with its own Topic. Simply adding a second Message and a second Topic to one `Telling` instance would leave it ambiguous which Topic belongs to which Message, so the frame is duplicated instead: two `Telling` instances on the same LU (`submit.v`), each with its own Message/Topic pair, while Speaker and Addressee (identical for both) are linked the same way on both instances.
> *(Instance 1)* __The Commission__ [Speaker] shall submit __a report__ [Message] to __the European Parliament__ [Addressee] and to __the Council__ [Addressee] __on the use of and benefits from those refinancing operations and funding support measures for credit institutions authorised in the Union__ [Topic].
> *(Instance 2)* __The Commission__ [Speaker] shall submit, together with __a legislative proposal__ [Message], to __the European Parliament__ [Addressee] and to __the Council__ [Addressee] __on the use of such refinancing operations and funding support measures if appropriate__ [Topic].

### 5.2 Intentionally_create
**Definition.** A Creator, through an intentional act, produces a Created_entity.

**Frame Elements used:** `Creator` (not yet observed to repeat in the corpus), `Created_entity` (not yet observed to repeat), `Purpose` (not yet observed to repeat).

**`Intentionally_create` never takes a `Topic` FE.** `Topic` belongs only to `Telling` (§5.1); `Intentionally_create` can take `Purpose` instead. See the `Telling` section above for the full distinction and the Creator/Speaker, Created_entity/Message caution.

**When to use it.** Only when the text requires the artifact to be *developed/drafted/produced*, as a step distinct from (and usually prior to) submitting it. If the text only mentions submission/delivery of an already-existing artifact, do not add `Intentionally_create`.

**Worked example:**
> *__ESMA__ [Creator] shall develop __draft regulatory technical standards__ [Created_entity] __to specify situations where...__ [Purpose]*
LU: `develop.v`.

### 5.3 Conditional_scenario
**Definition.** A Consequence is dependent on one or more Profiled_possibility conditions.

**Frame Elements used:** `Profiled_possibility` (repeatable for coordinated conditions), `Consequence` (not yet observed to repeat in the corpus).

**When to use it.** Triggered by conditional connectives (*if, where, unless, in the event that*). When two conditions are joined by "and"/"or", tag each as a separate `Profiled_possibility` link, mirroring the coordination rule in §4.5.

**Worked example:**
> *Where __such Union-wide assessments are carried out__ [Profiled_possibility] and __the Authority considers it appropriate to do so__ [Profiled_possibility], it shall __disclose the results__ [Consequence].*
LU: `where.adv`.

### 5.4 Time_vector
**Definition.** Locates an Event in time, at a Direction (before/after) and, optionally, a Distance, relative to a Landmark_event.

**Frame Elements used:** `Event`, `Direction` (does not repeat), `Landmark_event`, `Distance` (does not repeat).

**Rule:**
- `Landmark_event` = the reference point itself: a calendar date, or a named event ("the entry into force of this Regulation", "the end of each financial year"). Use this whenever the text gives a bare date or reference event with **no explicit numeral duration**.
- `Distance` = an explicit numeral + unit duration measured *from* a landmark ("30 days", "three months"). Use `Distance` together with `Landmark_event` when the text gives both (e.g. "within 30 days [Distance] of the end of the financial year [Landmark_event]"). Immediacy adverbs with no numeral (*immediately, promptly, without delay, forthwith*) are also tagged `Distance`, representing a near-zero duration, matching the corpus's existing `without_delay.adv` precedent, do not tag these `Direction`.
- `Direction` = the word/phrase expressing the before/after relation itself (by, after, from, not later than, within).
- `Event` = the clause whose timing is being constrained (start at the verb, per §4.6).

**Worked example:**
> *ESMA shall __submit those draft regulatory technical standards to the Commission__ [Event] at the latest __by__ [Direction] __2016-12-31__ [Landmark_event].*

### 5.5 Frequency
**Definition.** An Event recurs at a certain rate.

**Frame Elements used:** `Event` (does not repeat within one instance; see rule below).

**Rule:** `Event` must always be linked. Two cases:
- *Adverbial LU modifying a verb* (e.g. "at least annually", "quarterly"): `Event` = the governed clause, starting at the verb (§4.6).
- *Adjectival LU modifying an event-denoting noun* (e.g. "annual report", "quarterly report"): `Event` = that noun. If an FE span already exists for that noun for another frame (e.g. the `Message` of `Telling`), reuse it rather than creating a duplicate (§4.3).

**Worked example:**
> *At least __annually__ [LU], the Authority shall __consider whether it is appropriate to carry out Union-wide assessments...__ [Event]*

### 5.6 Artifact
**Definition.** Describes the reported object and, where relevant, its part-whole structure.

**Frame Elements used:** `Artifact` (does not repeat), `Artifact_subpart` (repeatable), `Artifact_superpart`.

**When to use it.** Use `Artifact`/`Artifact_subpart` when a provision specifies that a report must *include* or *contain* certain components. Use `Artifact_superpart` (with the complex preposition LU `as_part_of.prep`) when the text says the reported item is delivered *as part of* a larger document.

**Worked example:**
> *__That information__ [Artifact] shall include __a cost breakdown related to the previous year__ [Artifact_subpart] and __a forecast for the following year__ [Artifact_subpart].*

---

## 6. Quick reference: key decision rules

1. **Time_vector dates:** if the text gives just a date or reference point with no explicit duration (e.g. "by 2018-07-21"), tag it `Landmark_event`. If the text gives an explicit amount of time (e.g. "within 30 days"), tag that amount `Distance` and if a reference point is also named (e.g. "within 30 days of the end of the financial year"), tag that separately as `Landmark_event` too, so the two can co-occur on the same Time_vector instance. Immediacy adverbs with no numeral (immediately, promptly, without delay) are also `Distance`, not `Direction`.
2. **Frequency:** the `Event` FE must always be linked. If the frequency word is an adverb modifying a verb (e.g. "shall report **annually**"), `Event` = the verb's clause. If it is an adjective modifying a noun that itself names the recurring artifact (e.g. an "**annual** report"), `Event` = that noun (reuse its span from another frame if one already exists, e.g. `Telling`'s `Message`).
3. **Telling scope:** deliberately broad, covers any act of delivering/attaching/supplying report-like content to a recipient, not just canonical speech-act verbs.
4. **Coordinated fillers:** one FE span + one role-link per conjunct, never one span over the whole coordinated phrase.
5. **Span reuse:** if the same span of text is the correct filler for a role in two different frame instances, whether two instances of the same frame (e.g. one `Event` shared by two `Time_vector` instances, §4.3) or two different frames (e.g. a `Telling` Message that is also an `Artifact` frame's Artifact), create the FE span once and link both frames to it, rather than creating two separate copies of the same span.
6. **Event-span boundaries:** start at the verb, exclude subject and modal, *except* when the verb is passive with no separate agent, in which case include the subject (§4.6).
7. **Anaphora:** tag the mention closest to the LU, not the most explicit one.
8. **Supporting frames:** `Time_vector`, `Frequency`, `Artifact`, and `Conditional_scenario` are only annotated when they characterize a `Telling` or `Intentionally_create` instance, never on their own.
9. **Coordination vs. duplication:** repeat a role on one frame instance for simple coordinated fillers (§4.5); duplicate the Frame annotation instead when each filler needs its own distinct value for another role (§4.8).
10. **"In cooperation with X":** does not make X a Speaker/Creator, tag only the primary grammatical subject as Speaker/Creator (§4.9).
11. **Implicit agents:** both `Telling`'s Speaker and `Intentionally_create`'s Creator can be left unlinked when the sentence gives no explicit agent (agentless passive); do not guess one in.

---

## 7. Step-by-step procedure in INCEpTION

1. Read the whole provision once before annotating anything.
2. For each clause that evokes one of the six frames: mark the LU span, set its `lemma.POS` value.
3. Mark the Frame span (identical to the LU span), set the `Frame` feature.
4. For each core Frame Element you can identify in the text: select its span, create an `FE` annotation, then link it to the correct role from the Frame annotation's role list.
5. Check: did you reuse an existing FE span where the same text fills a role in a second frame, instead of duplicating it?
6. Check: for coordinated fillers, did you create one span + one link per conjunct?
7. Move to the next frame-evoking expression in the same provision and repeat.
8. Before closing the document, re-read it once fully annotated and verify every `Telling`/`Intentionally_create` instance has its core roles (Speaker/Creator at minimum) filled, and every `Time_vector`/`Frequency` instance has `Event` filled.
