## Business Requirements

Our company has 300 students that need to use an AI model to better commit to coursework and study for exams. Due to cyber attemps, we do believe that we need to have an internal LLM.

## Functional Requirements

The company wants to invest in owning their infrastructure.
The reason is because there is a concern about privacy of user data and also a concern that the cost of managed services for GenAI will greatly raise in cost. 

They want to invest an AI PC where they can afford spend of 10-15K
They have 300 active students, and students are located within the city of Nagasaki.

## Non-functional Requirements

This AI model needs to be reliable, cost-efficient, secure.

## Risks

There are some risks. 

AI is a new market and we need to make sure that we have trained professionals to implement and maintain. There is a risk of failure due to knowledge.
There is also a risk of cost. AI should be in the cost range to implement this solution, however, AI can grow expodentially due to misconfiguration and vastly increase cost in a second. 

## Assumptions 

We are assuming that the Open-source LLMs that we choose will be powerful enough to run on hardware with an investment of 10-15K.

We're going to hook up a single server in our office to the internet and we should have enough bandwidth to serve the 300 students.

## Data Strategy 

There is a concern of copyrighted materials, so we must purchase and supply materials and store them in our database. 

## Considerations

We're considering using IBM Granite because its a truely open-source model with training data that is tracable so we can avoid any copyright issues and we can know what exactly is going on in the model. 

https://huggingface.co/ibm-granite
