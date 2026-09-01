SARL Exception Handling for Multi-Agent Systems

This repository contains the implementation developed for my Master's thesis in Computer Science at the University of Turin:

"Development of Exception Management Strategies in Multi-Agent Systems: the SARL Case Study"

The project explores exception-handling strategies for multi-agent systems (MAS), with a focus on the SARL agent-oriented programming language.


Overview

Exception handling in multi-agent systems is more complex than in traditional software because agents are autonomous and may fail, communicate incorrectly, or become unavailable while other agents continue to operate.
The main idea explored in this project is an Exception Space: a dedicated event space in which agents can register with different responsibilities:
Raiser: an agent authorized to raise a specific exception.
Handler: an agent responsible for handling that exception.
This separates the agent that detects or raises a failure from the agent that is responsible for recovering from it.


Exception Space

The core abstraction is defined by ExceptionSpace<T extends Failure>.
It provides operations for:
- registering an agent as an exception raiser;
- registering an agent as an exception handler;
- raising an exception;
- removing an unavailable handler.

The implementation also handles two relevant failure conditions:
NoHandlerAvailable: no handler is registered for the raised exception;
NoSpecificHandlerAvailable: an exception is addressed to a specific agent that is not available as a handler.

Exceptions may therefore be propagated to all registered handlers or directed to a specific handler when required by the protocol.


Case Studies

The proposed mechanism was evaluated through several multi-agent scenarios.

Contract Net Protocol (CNP)
The repository contains an implementation of the Contract Net Protocol with exception-management strategies for situations such as:
- messages that are not understood;
- participants unable to complete an assigned task;
- absence of offers;
- ties between offers;
- unavailable handlers.

Recovery strategies allow the protocol, when possible, to exclude a failing participant, request new offers, select another participant, or terminate safely when recovery is not possible.
A version of the protocol without the exception-handling extensions is also included for comparison.

NetBill
The NetBill case study models a multi-agent electronic transaction and introduces failure scenarios involving:
- authorization and permission failures;
- missing or delayed updates;
- communication problems;
- unexpected agent termination;
- replacement of an unavailable agent when recovery is possible.

One recovery scenario uses checkpoint information to allow another agent to continue a transaction after the original agent becomes unavailable.

A version without the exception-handling extensions is included as well.

Treatment Scenario
-A smaller doctor-patient-pharmacist example implements fault-tolerance patterns such as:
-Checkpoint
-Remind
-Continue

The scenario demonstrates how agents can exchange intermediate information and recover from communication failures.


Project Structure

sarlexceptions/
├── events/
│   ├── ExceptionHandlerRegistered.sarl
│   ├── ExceptionRaiserRegistered.sarl
│   ├── ExceptionSpaceCreated.sarl
│   ├── NoHandlerAvailable.sarl
│   └── NoSpecificHandlerAvailable.sarl
│
├── spaces/
│   ├── ExceptionSpace.sarl
│   ├── ExceptionSpaceImpl.sarl
│   └── ExceptionSpaceSpecification.sarl
│
└── examples/
    ├── cnp/
    ├── cnpNoExecption/
    ├── netBill/
    ├── netBillNoException/
    └── treatment/

spaces/ contains the Exception Space abstraction and implementation.
events/ contains the events used by the exception-management mechanism. 
examples/ contains the case studies and comparison implementations.


Technologies

SARL --- agent-oriented programming language

Janus --- runtime/platform used by SARL multi-agent applications


Academic Context

This project was developed as part of my Master's thesis in Computer Science at the University of Turin, academic year 2023/2024.

The thesis investigates whether assigning explicit exception-management responsibilities to agents through raiser/handler registration can improve the robustness and resilience of multi-agent protocols.

The main case studies are the Contract Net Protocol and NetBill, together with a smaller treatment scenario used to explore recurring fault-tolerance patterns.

Andrea Traina
