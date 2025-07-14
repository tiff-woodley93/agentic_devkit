# Agentic DevKit

A development framework that leverages agents to implement, analyze, and manage component completion through a structured workflow.

## Overview

The Agentic DevKit provides a standardized approach to component-based development using AI agents. It integrates with Cursor IDE and uses a memory-based knowledge system to maintain context across development sessions.

## Quick Start

### 1. Initial Setup

1. **Initialise the component SDK template** you're using for your project
2. **Start the Basic Memory MCP server**:
   ```bash
   docker compose -f docker-compose-basic-memory.yml up
   ```

### 2. Configure Cursor IDE

Add the MCP server to your Cursor configuration:

```json
{
  "mcpServers": {
    "basic-memory": {
      "url": "http://localhost:8000/mcp"
    }
  }
}
```

Add the following to your cursor rules

```bash
The user will provide a MODE and COMPONENT_TYPE 

The agentic devkit notes can be found in the basic memory server under the COMPONENT_TYPE project.

If MODE: IMPLEMENT

Implement the task described in the agentic_devkit task.md.Follow best practices from the good_practice.md.

To understand the current progress and determine what steps may come next, refer to the state and next_steps notes, they will have an associated datetime in their name, pull the latest one.

Document all outputs produced in the contract_outputs.md, following the provided example in the note.

If you create tests, document them in plain English in tests.md.

After implementation:When working through the problem make sure to consitently add memory files by creating notes with the current datetime in the heading

state.md → Describe the current state of the project in a summarised fashion
next_steps.md → Provide a clear list of recommended next steps.Keep it summarised.

If the task is completed, update add memory files with the current datetime in the heading:

state → Describe the final state.
next steps → Confirm that all necessary steps have been completed.

Expected inputs for the task can be found in the note contract_inputs.md. If the inputs are not what are outlined in the expected inputs, stop and flag that the task can't be completed until the inputs meet the expectations.

All outputs produced must be documented in the contracts_outputs.md, following the example provided there.

To verify adherence to best practices, consult the feedback from the pre-commit hook for guidance, it can be run using:

pre-commit run --all-files 

If MODE: EXPLAIN

Analyze the current project setup by reviewing notes in the agentic dev kit, state.md, next_steps.md and task.md.  Provide a comprehensive explanation of the current architecture, task goals, existing progress, and the intended workflow.

If MODE: STATUS

From the agentic devkit read stat.md and next_steps.md.Summarize:The current state of the project.Any pending or recommended next steps based on the recorded memory.

If MODE: UPDATE

Make updates or additions to the project based on user's given instructions, using full context from:

- The existing codebase 
- The agentic_devkit notes - state.md, next_steps.md, task.md, best_practice.md

Document any changes clearly in the relevant memory and output files.

To verify adherence to best practices, consult the feedback from the pre-commit hook for guidance, it can be run using:

pre-commit run --all-files 

If MODE: CRITIC

Analyze the current project setup by reviewing notes in the agentic dev kit, state.md, next_steps.md and task.md.  Provide a comprehensive explanation of the current architecture, task goals, existing progress, and the intended workflow. Also provide a critic of what has been done, potential risks and suggest improvements

If MODE: RUN

Analyze the current project setup by reviewing notes in the agentic dev kit, state.md, next_steps.md and task.md. Provide steps of how to run the setup
```

### 3. Set Up Project Structure

1. **Configure pre-commit hooks** by setting up your `commit.yaml` to enforce best practices (** TO ADD Starter templates for each component)

2. **Initialize knowledge base** for your component type:
   - `best_practice.md` - Component-specific best practices (** TO ADD md for each component)
   - `contract_inputs.md` - Expected inputs for the task (** TO ADD example for each component)
   - `contract_outputs.md` - Documentation templates for outputs (** TO ADD example for each component)
   - `task.md` - Define the specific task to implement

## Usage

### Command Structure

Interact with the system using:
```
MODE: [COMMAND]
COMPONENT_TYPE: [Ingest/Enrich/Serve]
```

### Available Modes

#### `IMPLEMENT`
Implements the task described in `task.md` following best practices.

**Process:**
- Reviews current progress from latest `state.md` and `next_steps.md`
- Follows guidelines in `good_practice.md`
- Documents outputs in `contract_outputs.md`
- Creates tests and documents them in `tests.md`
- Updates state and next steps with current datetime

**Example:**
```
MODE: IMPLEMENT
COMPONENT_TYPE: Ingest
```

#### `STATUS`
Provides a summary of current project state and pending next steps.

**Output:**
- Current project state from `state.md`
- Recommended next steps from `next_steps.md`

#### `EXPLAIN`
Analyzes and explains the current project setup comprehensively.

**Covers:**
- Current architecture
- Task goals
- Existing progress
- Intended workflow

#### `UPDATE`
Makes targeted updates or additions based on specific instructions.

**Context Sources:**
- Existing codebase
- Agentic devkit notes
- State and next steps documentation
- Task definitions and best practices

#### `CRITIC`
Provides critical analysis of the current implementation.

**Analysis Includes:**
- Architecture review
- Risk assessment
- Improvement suggestions
- Best practice adherence

#### `RUN`
Provides step-by-step instructions for running the current setup.


### Documentation Standards
All implementations must:
- Document outputs in `contract_outputs.md`
- Update state tracking with timestamps
- Follow the provided templates
- Include plain English test descriptions if implemented

## Devkit Structure

```
├── task.md                 # Main task definition
├── best_practice.md        # Component-specific guidelines
├── contract_inputs.md      # Expected input specifications
├── contract_outputs.md     # Output documentation templates
├── state.md               # Current project state (timestamped)
├── next_steps.md          # Recommended next actions (timestamped)
└── tests.md               # Test documentation
```

## Troubleshooting

- **Input validation**: If inputs don't match `contract_inputs.md`, implementation will halt
- **Memory server**: Ensure Basic Memory MCP server is running on `localhost:8000`


