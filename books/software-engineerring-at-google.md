Notes made when reading https://abseil.io/resources/swe-book

# What is Software Engineering

* Software engineering - programming integrated over time. It's not programming
* There's a factor of at least 100,000 times between short- and long-lived code
* Hyrum's Law - with sufficient number of users of an API, it doesn't matter what you promise in the contract: all
  observable behaviors of your system will be depended on by somebody.
* It's programming if 'clever' is a compliment, it's software development if 'clever' is an accusation
* Churn Rule - infra teams must do the wrk to move their internal user to new versions themselves or do the update in
  place, in backward-compatible fashion
* Beyonce Rule - If you liked it, you should have put a CI test on it. In other words: if no CI tests break when a
  dependency is changed, it's the fault of the authors of the code, not the infra team
* Shifting Left - finding problems earlier reduces their costs
* Even if there isn't _data_, there can still be _evidence_, _precedent_ and _argument_
* Jevons paradox - consumption of a resource might increase as a response to greater efficiency in its use
* Software is sustainable when for the expected life span of code, we are capable of responding to changes no
  dependencies, technology, or product requirements. We may choose not to change, but we need to be capable.
* Every task in your org that has to be done repeatedly has to be scalable (linear or better) in terms of human input.
  Policies can be very useful in that.
* Inefficiencies in process or other tasks can scale up slowly (boiling frog)
* Being data-driven over time implies changes needed over time

# How to work well on teams

* Software engineering is a team endeavor 
* People tend to want to hide their work/code. This is because of a Genius Myth - we want to look like geniuses, coming
  up with ready and polished solutions and not sharing the initial states. This is a wrong way to work as a Software Engineer. This is because:
  * You don't know if you doing the right thing (early detection)
  * You're causing a Bus Factor. It's better to be a small part of a successful project than a critical part of a failing one.
  * The feedback loop is long. Many eyes make all bugs shallow.
* In short: don't hide.
* The Three Pillars of Social Interaction:
  * Humility
  * Respect
  * Trust
* 
*
* 