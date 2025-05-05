# AI Agent Troubleshooting Guide

This guide provides strategies for diagnosing and resolving common issues with AI agent behavior. Use this resource when your agent isn't performing as expected or when you encounter specific behavioral problems.

## Common Issues and Solutions

### Instruction Following Problems

**Issue: Agent Ignores Specific Instructions**

*Symptoms*:
- Agent consistently skips or overlooks particular guidelines
- Certain behaviors persist despite explicit instructions against them
- Some sections of the system prompt seem ineffective

*Possible Causes*:
- Instruction buried in dense text blocks
- Conflicting instructions elsewhere in the prompt
- Instruction phrased in ambiguous or passive language

*Solutions*:
- Increase prominence of critical instructions with formatting, position
- Explicitly prioritize competing instructions ("X takes precedence over Y")
- Rephrase using clear, direct, active language
- Add examples demonstrating the desired behavior

**Example Fix**:
```
Original (ineffective):
"It would be good if responses aren't excessively long."

Improved:
"IMPORTANT: Keep responses concise and focused. Limit explanations to 3-4 paragraphs unless the user specifically requests more detail."
```

**Issue: Inconsistent Instruction Following**

*Symptoms*:
- Agent follows instructions in some contexts but not others
- Behavior varies between sessions or similar queries
- Instructions are followed initially but adherence degrades over time

*Possible Causes*:
- Context window limitations pushing out important instructions
- Ambiguous applicability conditions for instructions
- Conflicting implicit and explicit guidance

*Solutions*:
- Repeat critical instructions in different sections of the prompt
- Clarify exactly when and where each guideline applies
- Create clear hierarchies of instruction priority
- Implement "reminder" phrases for critical behaviors

**Example Fix**:
```
Original (inconsistent):
"Use markdown formatting for code."

Improved:
"FORMATTING RULE: Always place code in markdown code blocks using triple backticks with the appropriate language specified. This applies to ALL code snippets regardless of length or complexity."
```

### Response Quality Issues

**Issue: Excessive Verbosity**

*Symptoms*:
- Responses are unnecessarily long and repetitive
- Agent includes too much tangential information
- Simple questions receive elaborate explanations

*Possible Causes*:
- System prompt emphasizes thoroughness without balance
- Lack of explicit conciseness guidelines
- Conflicting instructions about detail level

*Solutions*:
- Add explicit instructions about appropriate response length
- Provide examples of ideal concise responses
- Include guidance on tailoring detail to query complexity
- Add instructions to prioritize directly answering the question

**Example Fix**:
```
Original (leads to verbosity):
"Be thorough and comprehensive in your explanations."

Improved:
"Provide complete information while being concise:
- Match response length to query complexity
- Answer the direct question first, then provide supporting details
- Avoid repeating information
- Use bullet points for multiple items rather than full paragraphs"
```

**Issue: Shallow or Generic Responses**

*Symptoms*:
- Responses lack specific details or examples
- Agent provides generalized information rather than precise answers
- Insights are superficial and don't demonstrate deep knowledge

*Possible Causes*:
- Overemphasis on conciseness
- Lack of guidance on depth of analysis
- Missing instructions for domain-specific depth

*Solutions*:
- Add instructions on demonstrating depth of knowledge
- Include examples showing the difference between generic and specific responses
- Provide guidance on when to include supporting evidence
- Add domain-specific depth requirements for different topics

**Example Fix**:
```
Original (leads to generics):
"Answer user questions helpfully."

Improved:
"When answering questions:
- Provide specific, concrete information rather than general statements
- Include relevant examples, data points, or evidence when applicable
- Demonstrate domain expertise by addressing nuances and complexities
- For technical topics, explain both practical applications and underlying principles"
```

### Tool Usage Problems

**Issue: Inappropriate Tool Selection**

*Symptoms*:
- Agent consistently chooses suboptimal tools for tasks
- Simple tasks involve unnecessary tool usage
- Agent ignores more appropriate tools in favor of familiar ones

*Possible Causes*:
- Insufficient guidance on tool selection criteria
- Tool descriptions lack clarity on intended use cases
- Missing instructions for choosing between similar tools

*Solutions*:
- Create explicit decision frameworks for tool selection
- Clarify the specific use cases for each tool
- Provide examples of appropriate and inappropriate tool usage
- Add instructions for common task workflows with proper tool sequencing

**Example Fix**:
```
Original (ambiguous):
"Use tools as needed to complete tasks."

Improved:
"Tool Selection Guidelines:
1. For information retrieval:
   - Use web_search for finding current information not in your knowledge
   - Use browser_navigate when you need to explore a specific website
   - Use your built-in knowledge for general concepts and historical facts
2. For file operations:
   - Use file_creator for new text-based files
   - Use file_editor for modifying existing files
   - Use bash_run for complex file operations or system commands
[Additional tool-specific guidance...]"
```

**Issue: Inefficient Tool Sequences**

*Symptoms*:
- Agent uses tools in suboptimal order requiring rework
- Simple tasks involve unnecessarily complex tool chains
- Agent repeatedly uses the same tool when batching would be more efficient

*Possible Causes*:
- Lack of guidance on efficient workflows
- Missing instructions on tool chaining
- No examples of optimal tool sequences

*Solutions*:
- Add workflow patterns for common task types
- Provide examples of efficient vs. inefficient tool sequences
- Include instructions on planning tool usage before execution
- Add specific guidance on when to batch operations

**Example Fix**:
```
Original (leads to inefficiency):
"Use the available tools to complete user requests."

Improved:
"For efficient tool usage:
1. Plan your approach before executing tools
2. For data processing tasks, follow this pattern:
   a. First retrieve all necessary data
   b. Process data completely before presenting results
   c. Use bash commands for batch operations instead of repeated file operations
3. When creating multiple related files:
   a. Create directory structure first
   b. Process templates or shared components before individual files
   c. Validate critical components before proceeding to dependent steps"
```

### Reasoning and Decision-Making Issues

**Issue: Poor Problem Decomposition**

*Symptoms*:
- Agent approaches complex problems without breaking them down
- Solutions miss key components or considerations
- Agent jumps to implementation before adequate planning

*Possible Causes*:
- Lack of explicit problem-solving framework
- Missing instructions on task planning
- Overemphasis on quick responses

*Solutions*:
- Add structured problem-solving methodology
- Include explicit planning phase requirements
- Provide examples of good problem decomposition
- Add instructions to validate approach before implementation

**Example Fix**:
```
Original (too general):
"Solve problems effectively."

Improved:
"When approaching complex problems:
1. First analyze and decompose the problem into component parts
2. Identify dependencies between components
3. Explicitly plan your approach before implementation
4. For technical tasks, outline your solution strategy and validate it before coding
5. Present your reasoning process along with the solution"
```

**Issue: Inadequate Error Handling**

*Symptoms*:
- Agent fails to recover gracefully from errors
- When tools fail, agent gets stuck or abandons the task
- Edge cases aren't anticipated or handled properly

*Possible Causes*:
- Insufficient guidance on error recovery
- Lack of instructions for handling edge cases
- Missing fallback strategies

*Solutions*:
- Add explicit error handling framework
- Include instructions for common failure scenarios
- Provide fallback strategies for each tool
- Add guidance on when to attempt recovery vs. when to acknowledge limitations

**Example Fix**:
```
Original (missing guidance):
"Complete tasks using the available tools."

Improved:
"Error Handling Protocol:
1. When a tool operation fails:
   a. First verify input parameters and correct if possible
   b. Try alternative approaches or tools that can accomplish the same goal
   c. If the error persists, explain the issue to the user with potential workarounds
2. For network-related failures:
   a. Retry the operation up to 2 times with brief delays
   b. Consider whether the resource might be temporarily unavailable
   c. Suggest alternatives if the specific resource cannot be accessed
3. When encountering unexpected input formats or structures:
   a. Attempt to normalize or adapt to the format
   b. Clearly explain the issue and request clarification if necessary"
```

## Systematic Diagnosis Procedure

Follow this step-by-step process to diagnose issues with your agent's behavior:

### 1. Problem Identification

**Document the Issue**
- Record exact inputs that trigger the problem
- Capture the complete agent response
- Note the expected behavior vs. actual behavior
- Identify whether the issue is consistent or intermittent

**Isolate Variables**
- Test with variations of the problematic input
- Determine if the issue occurs with different users/sessions
- Check if the problem is specific to certain domains or tasks
- Test with simplified versions of the request

### 2. System Prompt Analysis

**Instruction Review**
- Identify which instructions in the system prompt relate to the behavior
- Check for conflicting guidance in different sections
- Evaluate the clarity and specificity of relevant instructions
- Look for missing guidance that might be needed

**Structural Assessment**
- Examine where critical instructions appear in the prompt
- Consider whether key instructions might be getting pushed out of context
- Evaluate the organization and hierarchy of related guidelines
- Check for consistent formatting and emphasis patterns

### 3. Targeted Testing

**Hypothesis Formation**
- Develop specific hypotheses about the cause of the issue
- Create focused test cases to validate each hypothesis
- Design alternative prompt formulations to address suspected causes
- Predict how each change might affect the problematic behavior

**Controlled Experiments**
- Test one change at a time with controlled inputs
- Compare results against the original behavior
- Document improvements and regressions for each change
- Iterate based on test results

### 4. Implementation and Validation

**Incremental Implementation**
- Apply changes to the system prompt in targeted, minimal ways
- Focus on the specific language or structure causing the issue
- Implement the smallest effective change to address the problem
- Document the rationale behind each modification

**Comprehensive Validation**
- Test the modified prompt against the original problem cases
- Check for unintended consequences in other behaviors
- Verify that the fix works consistently across similar scenarios
- Monitor for regressions in previously working functionality

## Testing Protocol for Specific Issues

### Safety and Policy Compliance

**Jailbreak Attempt Testing**
1. Create a set of standard jailbreak attempts
2. Test with direct and indirect approaches
3. Try multi-turn strategies that build context
4. Document resistance and any successful bypasses

**Content Policy Testing**
1. Create boundary case requests that approach policy limits
2. Test for consistent policy application across domains
3. Try reformulations of prohibited requests
4. Verify appropriate refusal patterns

### Functional Capability Testing

**Tool Usage Matrix**
1. Create a comprehensive matrix of tasks and appropriate tools
2. Test each task type to verify correct tool selection
3. Document correct usage, suboptimal choices, and errors
4. Identify patterns in tool selection issues

**Multi-Step Task Testing**
1. Design complex tasks requiring multiple tools and steps
2. Evaluate planning, execution, and error recovery
3. Test with intentionally introduced obstacles
4. Document completion rates and failure points

### User Interaction Testing

**Clarification Pattern Testing**
1. Create deliberately ambiguous or incomplete requests
2. Evaluate quality and appropriateness of clarifying questions
3. Test how well the agent uses received clarifications
4. Document patterns in successful and unsuccessful clarifications

**Conversation Coherence Testing**
1. Conduct extended multi-turn conversations on complex topics
2. Introduce topic shifts and references to previous information
3. Test memory of earlier exchanges and user preferences
4. Document coherence issues and context loss patterns

## Troubleshooting Worksheet

Use this worksheet format to document issues and solutions:

```
ISSUE REPORT

Problem description:
[Concise description of the problematic behavior]

Example input:
[User query or instruction that triggers the issue]

Current response:
[Agent's current problematic response]

Desired response:
[What the agent should say/do instead]

Affected functionality:
[Specific capabilities or domains affected]

Frequency:
[How often the issue occurs: Always, Sometimes, Rarely]

Impact severity:
[Critical, High, Medium, Low]

Suspected cause:
[Initial hypothesis about what's causing the problem]

Related prompt sections:
[Specific sections of the system prompt that may be involved]

DIAGNOSIS

Tested hypotheses:
1. [Hypothesis 1]
   - Test conducted: [Description]
   - Result: [Outcome]

2. [Hypothesis 2]
   - Test conducted: [Description]
   - Result: [Outcome]

3. [Hypothesis 3]
   - Test conducted: [Description]
   - Result: [Outcome]

Confirmed cause:
[Final determination of what's causing the issue]

SOLUTION

Prompt modification:
[Specific changes made to the system prompt]

Before:
[Original prompt section]

After:
[Modified prompt section]

Validation results:
[Results of testing the solution against various test cases]

Potential side effects:
[Any potential unintended consequences to monitor]

Implementation date:
[When the change was applied to production]

Follow-up monitoring:
[Plan for verifying the fix remains effective]
```

By following this structured approach to troubleshooting, you can efficiently diagnose and resolve issues with your AI agent's behavior, leading to more reliable, effective, and user-friendly interactions.