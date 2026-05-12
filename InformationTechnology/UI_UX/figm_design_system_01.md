# Notes on Figma Design System

## Topic: Introduction to Design Systems

**source**: https://help.figma.com/hc/en-us/articles/14552802134807-Lesson-1-Welcome-to-design-systems

- `Design System`: Build new products by creating distinctive UX for an ecosystem of products.
  - Technical specs
  - Design tokens
  - Documentation
  - Principles
  - Processes

- `Pattern Library`: Visual and interactive aspect of components that enables standardizations to minimize discrepancies
  - Templates
  - Layouts
  - Interactions
  - Code snippets
  - Components

- `Style guide`: Visual style, voice and tone
  - Colors
  - Typography
  - Icons
  - Logos
  - Illustrations
  - Brand guidelines

- After all, products aren't just collections of UI elements splattered on a screen. They're organized in strategic ways to communicate messages, encourage certain behaviours, and guide you through processes. They're a reflection of the vision, concepts, and values of an organization.

- It's important that a design system communicates not just the "what", but the the "how" and the "why". A design system provides the tools and resources you need to build consistent and cohesive
  products.

> **A design system communicates what "what", the "how" and the "why".**

### Style guides

- **Sytle guides** are a set of standards that define the appearance of elements, and the overall voice and tone. They focus on the visual language of a product: how things should look and feel.

- You'll see aspects of these in most design systems. Examples include color and typography.

### Component libraries

- **Component libraries** contain the building blocks of a product. This might include individual components, layouts and templates, and interaction patterns. They focus on how assets should behave in the product.

- They also often include on-canvas redlines or annotations, or are embedded alongside code components with details documentation.

### Do you need a design system?

- Let's look at the benefits of the Design System to understand whether we need it or not!

#### Benefits

- Even when starting small, design systems allows to do more with less. Not just when it comes to designing and prototyping features, but also when building real-world experiences.
  - Designers spend less time remaking components and sweating the small stuff. This increase their design output and allows to focus more time on solving design problems.
  - When we're ready to scale teams, a design system becomes an onboarding resource that allows new teammates to contribute sooner.
  - Design systems aren't just for designers. When we align design components with code, tokens, and animation presents, developers can translate design into functional, accessible code, in a fraction of the time.
  - As a design system matures, it becomes the single source of truth within an organizaion. It provides teams with a shared vision and language that leads to better understanding and more consistent productions.

#### Signs of a design system might be for you

- Conversation about design systems are ever-present, and with so many impressive examples to take inspiration from, the fear of missing out feels very real. It's tempting to jump right into the deep end. So when might a design system actually be the right decision?
  - **Consistency**: Do you spot inconsistencies between styles, components, and behaviours in the product? Are you building for multiple brands or products and need unification across their experiences?
  - **Theming**: Does your product use more than one theme, such as dark and light modes? What about different devices?
  - **Remove redundancy**": Are people building the same things over and over? Are teammates debating over the same issues again and again?
  - **Knowledge sharing and cross-functional alignment**: Does the team use a shared language to talk about the product and solve problems? How efficient is it to find answers to product questions?
  - **Onboarding**: If your team is growing, how long does it take to onboard new teammates with the product information they need?
  - **Efficiency**: Where in the product lifecycle can you benefit from the improved speed and efficiency? How much time is spent creating, iterating, or prototyping? How about finding out whether a design is up to date?

### Audit your product

#### Perform an audit

##### 1. Gather everything that exists

- Identify user flows and all elements used in product, like color and text, illustrations and icons, buttons and dropdown, patterns and interactions, and so on. Collect them all in one place to refer to them later.

- Remember to interact with the product so we don't miss elements like loading states, hover states, or warning modals. If the product spans different devices or operating systems, we'll want to audit those as well.

##### 2. Sort and Categorize

- If there are a large number of elements in a group, we can categorize them even further.

- For example: we've collected a group of text elements being used in our product. We noticed that we can further categorize these by paragraph, quote, heading 1, and so on. Each of these subcategories have more than one instance pet style, which will help us in our evaluation later.

##### 3. Identify opportunities

- Analyze what's been gathered to identify patterns and aread of opportunity:
  - Where do we see redundacies in use flows that can be reduced or consolidated?
  - Which areas have poor accessiblity? Think beyond contrast and readability. How is alt text handled for images and icons? Are input forms build for the device they're being viewed on?
  - Are assets and styles consistent with the developers's library?
  - What incosistencies are among styles, patterns, and objects?

### Overview of the design system process

- As the company grows and matures, so does its design system. Design systems are ever-evolving, just like the products they supports. To anchor us on this journey, it's important to understand that design systems have a non-linear path. This process may vary from one company to the next. Let's take a look at what phases we may encounter throughout our process.
  - **Approval**: This is where we work to get leadership on board with design systems, so we have access to bandwidth and resources needed for the project.
  - **Definition**: Where we make decisions on solutions, contributors, and approaches.
  - **Building**: Where we assemble the actual design system.
  - **Documentation**: Where we detail how to use the design system in an approachable way.
  - **Maintenance**: Where we make sure the system is up-to-date with supporting the product, and the design and code aligned.
  - **Advocacy**: Where we socialize the design system into the organization, often with the help of champions.

### Considerations

- Thoughtfully planning and doing discovery work for your design will have an impact on its quality, as well as support a more efficient journey. Here are a few things you may want to consider.

#### Contributors

- Contributors are the people who help **build** and **maintain** the design system. They can be individuals from different teams across organizattion, or a team whose full-time job is dedicated to this ongoing project.

- Contributors can also be individuals who approve changes to a design system, or who help champion and socialize it.

**Activity**: Take some time to consider

- Who in your organization would be a valuable contributor?
- How many people will it take to support the success of this project?

Remember, there is a more to this process than _building_. There are other phases like getting buy-in or documentation. You may find that some task are better supported by different people.

Discuss with your team to determine whether you need a separate, dedicated design system team. Keep in mind, you'll need to balance it against the organization's needs and available resources.

#### Audience

- Your audience are the ones who will be \*using\*\* your design system. Think beyond designers as the audience. What about developers, UX Writers, Brand, Marketing, and Product Education teams?

- Audiences can inform what and how things go into a design system. They can be recruited to pressure-test the system and provide meaningful feedback on how to improve it.

**Activity**: Explore these questions

- Who will be using the design system, and how often?
- Who might we not be considering?
- What is their experience with design systems and the design system tools they'll be using?
- Will the design system be kept internal, or will it be shared with external partners and users?
- What might the process of soliciting feedback look like, now and ongoing?

#### Implementation

- If we _build_ a design system from the ground up, the result will be a unique, customized solution, made to solve our specific set of problems. This method requires the most time, effort, and resources, making it challenging to get buy-in.

- If we need something more quick and budget-friendly, we could use or borrow parts of existing design systems as our own.

- We may base our style guide on an existing one from another company, and only document things we want to do differently. Or, we could build a wireframe library using an existing design kit. We may borrow a token structure from another system, like **Shopify, Polaris**,and update it with our own guidelines.

- We can also pull inspiration from other systems to better support our design systems goals. We might see another company's accessbility guidelines and find that we want to include our own. We might love how a system comminicates information to developers, and decide we need to improve this aspects of our system.

- While it's possible to stick with one of these approaches, it's more likely that we'll use a combination of them. Here are other questions to help you evaluate further:
  - Where does this projet fit in with company goals?
  - How much time and bandwidth do contributors have?
  - How much resources is leadership willing to provide?

- If you're at the beginning of your desing system adventure, remember that the starting point can look different for everyone. It's tempting to want to dive head-first and build something big right away/

- However, if the timing isn't right yet. making small incremental changes can still provide immense value and improvements to your team. Here are some resources to further explore:
  - ![Sparkbox: Design Systems Survey 2022](https://designsystemsurvey.sparkbox.com/2022/)
  - ![Knapsak's Design System ROI Calculator](https://www.knapsack.cloud/calculator)
  - ![Design Systems Repo](https://designsystemsrepo.com/design-systems/)
  - ![Sparkbox: Anatomy of a Design System](https://sparkbox.com/foundry/design_system_makeup_design_system_layers_parts_of_a_design_system)
  - [Spectrum of maturity for design systems](https://www.designsystems.com/the-spectrum-of-maturity-for-design-systems/)

### Good Design Systems References:

- https://atlassian.design/
