AWS CCP Certification is *not required for our program*, but we *will* be going over the content to get familiar with it.

**REQUIRED:**
Java ✅
ISTQB - An in-person exam, plan is to take the exam the end of week 5. (Aug. 9th)

For the rest of this week, we'll start going over testing material. **This will pertain to the ISTQB exam.** There probably won't be much live-coding, a lot of it will be PowerPoint material.

**There are practice exams online.** The exam also has a similar grade cutoff.

[https://www.istqb.org/certifications/certified-tester-foundation-level](https://www.istqb.org/certifications/certified-tester-foundation-level "https://www.istqb.org/certifications/certified-tester-foundation-level")

Exam Prep Resource - [This series goes over all of the content.](https://youtube.com/playlist?list=PLj5VKaW115t0LT-7DICjHkGuxdTEqFI91&si=84ZnPVwklSI6kYaB)

---

# Finishing React Content

*We're back in the Movie example.*

POST Request Example

Two types of components in React:
 - Built-in components, like `<div>` and `<span>`.
 - Custom (user-defined) components, which must start with an uppercase letter, e.g. `<MyComponent>`.

Important Attributes that Input elements need:
- Type - Specifies the type of `<input>`
- Name - Specifies the name of the element
- Value - Specifies the initial value of the element

 To stop refreshes, we can use `useRef`, or we can use `e.preventDefault`.
  - `e.preventDefault()` - A method on the event object `e`, used to prevent the default action of an event from happening, such as clicking on a link from navigating to a new page.
  - `useRef` is a hook in React that allows you to interact with the DOM nodes directly.

When `onSubmit` takes in `handleSubmit` as its argument, it will invoke that function and pass it the event object as the parameter so long as the function itself is passed to `onSubmit`.

With this code, `console.log` would be passed the event object.
```
<button onClick={console.log}>Click Me</button>
```

What does the `fetch()` method return?
 - It returns a promise. 
	 - Needs a `.then()`, and a `.catch()` to handle the two cases.

Note that RTK Query and React Query are nice APIs to work with for frontend stuff.

---

**For project 1, part of the grade *will be* based on the architecture.**

**Make sure to think out the design for the frontend, how the backend is built out, how databases are configured - all of that.**
### Definitely create separate components for Project 1 - don't just put everything in `App.jsx`!

