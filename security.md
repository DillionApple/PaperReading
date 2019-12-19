# Security

## Mobile Devices

### TextExerciser: Feedback-driven Text Input Exercising for Android Applications (CCS 2020) (2019-12-16)

The point of this paper is very interesting. It converts a UI testing problem into a security problem. More code coverage -> more chance to find security bugs.

It is hard to test text input components on apps cause they usually have constrains. Previous work does not consider these constrains and can not achieve higher code coverage rate. This work uses text input component feedbacks on App's screen to generate input texts which satisfies the constrains of the input component. This can achieve higher code coverage and may trigger potential secure bugs of the App.

It studied about 200 Apps. It classifies the input feedback texts colledted from these Apps into 4 major categories. It uses NLP and ML to analyze input component feedback texts and recognize the constrain in them to generate new input texts iteratively.