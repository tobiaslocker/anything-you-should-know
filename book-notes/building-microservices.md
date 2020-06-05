### Glossary 

|Term | Description |
|-----|-------------|
|Service-oriented architecture (SOA)|A design approach where multiple services collaborate to provide some end set of capabilities|
|Governance (COBIT) |Governance ensures that enterprise objectives are achieved by evaluating stakeholder needs, conditions and options; setting direction through prioritisation and decision making; and monitoring performance, compliance and progress against agreed-on direction and objectives|
|Loose Coupling |When services are loosely coupled, a change to one service should not require a change to another

### Chapter 2: The evolutionary Architect

#### Summary

> To summarize this chapter, here are what I see as the core responsibilities of the evolutionary architect

|Keyword |Description |
|--------|------------|
|Vision |Ensure there is a clearly communicated technical vision for the system that will help your system meet the requirements of your customers and organization|
|Empathy |Understand the impact of your decisions on your customers and colleagues|
|Collaboration |Engage with as many of your peers and colleagues as possible to help define, refine, and execute the vision|
|Adaptability |Make sure that the technical vision changes as your customers or organization requires it|
|Autonomy |Find the right balance between standardizing and enabling autonomy for your teams|
|Governance |Ensure that the system being implemented fits the technical vision|

### Chapter 4: Integration

#### Rest

> Most important is the concept of resources. You can think of a resource as a thing that the service itself knows about, like a Customer.

##### Hypermedia As the Engine of Application State

> Another principle introduced in REST that can help us avoid the coupling between client and server is the concept of hypermedia as the engine of application state (often abbreviated as HATEOAS, and boy, did it need an abbreviation)

##### A Hybrid Approach

> My clients often struggle with the question “Should I build, or should I buy?” In general, the advice I and my colleagues give when having this conversation with the average enterprise organization boils down to “Build if it is unique to what you do, and can be considered a strategic asset; buy if your use of the tool isn’t that special.”

#### Summary

> Summary We’ve looked at a number of different options around integration, and I’ve shared my thoughts on what choices are most likely to ensure our microservices remain as decoupled as possible from their other collaborators:

- Avoid database integration at all costs.
- Understand the trade-offs between REST and RPC, but strongly consider REST as a good starting point for request/response integration.
- Prefer choreography over orchestration.
- Avoid breaking changes and the need to version by understanding Postel’s Law and using tolerant readers.
- Think of user interfaces as compositional layers.

### Quotes

> Which is also why I view most forms of IT certification as worthless, as we know so little about what good looks like.

> To turn things around, if bridge building were like programming, halfway through we’d find out that the far bank was now 50 meters farther out, that it was actually mud rather than granite, and that rather than building a footbridge we were instead building a road bridge

> "be worried about what happens between the boxes, and be liberal in what happens inside"

> ...I called this onion architecture, as it had lots of layers and made me cry when we had to cut through it.

> ...short-term gain for long-term pain...

> “Be conservative in what you do, be liberal in what you accept from others.” - Postel’s Law (otherwise known as the robustness principle)
