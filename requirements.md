# Requirements Document

## Introduction

CodeMentor Live is an AI pair programming assistant designed to teach developers by predicting mistakes before they happen. The system targets junior to mid-level developers learning new codebases, providing real-time feedback through a VS Code extension, contextual explanations via Claude API, and personalized learning experiences based on skill gap analysis.

## Glossary

- **CodeMentor_System**: The complete AI pair programming assistant including VS Code extension, backend services, and AI integration
- **Thought_Process_Replay**: Feature that predicts common mistakes and demonstrates expert mental models
- **Codebase_Storytelling**: Feature that explains confusing code through git history and architectural decision analysis
- **Skill_Gap_Detector**: Feature that analyzes code patterns to identify weak concepts and generate challenges
- **VS_Code_Extension**: Frontend component providing real-time feedback within the VS Code editor
- **Backend_Service**: Node.js service coordinating AI requests, git analysis, and data persistence
- **Claude_API**: External AI service providing contextual code explanations
- **Git_Analysis_Engine**: Component that traces code history and extracts architectural decisions
- **Progress_Dashboard**: React-based web interface for tracking learning metrics
- **Skill_Level**: Developer proficiency categorization (junior, mid-level)
- **Mistake_Prediction**: AI-generated forecast of likely errors based on code context and skill level
- **Mental_Model**: Expert thinking pattern demonstrated to the user
- **Learning_Challenge**: Personalized coding exercise generated from identified skill gaps

## Requirements

### Requirement 1: Thought Process Replay

**User Story:** As a developer, I want the system to predict mistakes I might make and ask me what will happen, so that I can learn expert mental models before making errors.

#### Acceptance Criteria

1. WHEN a developer writes code in a context where common mistakes occur, THE CodeMentor_System SHALL identify potential mistakes based on the developer's skill level
2. WHEN a potential mistake is identified, THE CodeMentor_System SHALL prompt the developer with "What will happen if you do X?" before the mistake occurs
3. WHEN a developer responds to a prediction prompt, THE CodeMentor_System SHALL provide an expert mental model explanation
4. WHEN displaying mental models, THE CodeMentor_System SHALL include concrete examples relevant to the current code context
5. THE CodeMentor_System SHALL track prediction accuracy and adjust future predictions based on developer responses

### Requirement 2: Codebase Storytelling

**User Story:** As a developer, I want to understand confusing code by seeing its history and architectural decisions, so that I can learn why code was written a certain way.

#### Acceptance Criteria

1. WHEN a developer selects confusing code, THE CodeMentor_System SHALL retrieve the git history for that code section
2. WHEN git history is retrieved, THE Git_Analysis_Engine SHALL identify relevant commits, authors, and change patterns
3. WHEN architectural decisions are detected in commit messages or code changes, THE CodeMentor_System SHALL extract and present them
4. WHEN presenting code history, THE CodeMentor_System SHALL generate a narrative explanation connecting historical changes to current code structure
5. THE CodeMentor_System SHALL use the Claude_API to synthesize git history into human-readable storytelling format

### Requirement 3: Skill Gap Detection

**User Story:** As a developer, I want the system to identify my weak concepts and generate personalized challenges, so that I can improve specific skills.

#### Acceptance Criteria

1. WHEN a developer writes code, THE Skill_Gap_Detector SHALL analyze code patterns to identify recurring issues
2. WHEN code patterns are analyzed, THE Skill_Gap_Detector SHALL map issues to specific programming concepts
3. WHEN weak concepts are identified, THE CodeMentor_System SHALL generate personalized learning challenges targeting those concepts
4. THE CodeMentor_System SHALL track concepts mastered per week and display progress metrics
5. WHEN generating challenges, THE CodeMentor_System SHALL ensure challenges are appropriate for the developer's current skill level

### Requirement 4: Real-Time VS Code Integration

**User Story:** As a developer, I want to receive feedback directly in my editor, so that I can learn without context switching.

#### Acceptance Criteria

1. THE VS_Code_Extension SHALL integrate with the VS Code editor environment
2. WHEN code is written or modified, THE VS_Code_Extension SHALL send code context to the Backend_Service in real-time
3. WHEN feedback is received from the Backend_Service, THE VS_Code_Extension SHALL display it as inline suggestions, hover tooltips, or sidebar panels
4. THE VS_Code_Extension SHALL provide UI controls for interacting with Thought Process Replay prompts
5. WHEN a developer selects code, THE VS_Code_Extension SHALL enable triggering Codebase Storytelling analysis

### Requirement 5: Backend Service Coordination

**User Story:** As a system architect, I want a backend service to coordinate AI requests and git analysis, so that the system can process complex operations efficiently.

#### Acceptance Criteria

1. THE Backend_Service SHALL receive code context and analysis requests from the VS_Code_Extension
2. WHEN analysis requests are received, THE Backend_Service SHALL coordinate calls to the Claude_API for AI-powered explanations
3. WHEN git history is needed, THE Backend_Service SHALL invoke the Git_Analysis_Engine
4. THE Backend_Service SHALL persist developer progress data, skill assessments, and learning metrics
5. THE Backend_Service SHALL return processed results to the VS_Code_Extension within 2 seconds for real-time feedback

### Requirement 6: Claude API Integration

**User Story:** As a developer, I want contextual AI-powered explanations, so that I receive high-quality learning content.

#### Acceptance Criteria

1. WHEN the Backend_Service requests explanations, THE CodeMentor_System SHALL send code context and developer skill level to the Claude_API
2. WHEN generating mistake predictions, THE CodeMentor_System SHALL use the Claude_API to create skill-appropriate predictions
3. WHEN generating mental model explanations, THE CodeMentor_System SHALL use the Claude_API to produce clear, educational content
4. WHEN synthesizing git history, THE CodeMentor_System SHALL use the Claude_API to create narrative explanations
5. IF the Claude_API is unavailable, THEN THE CodeMentor_System SHALL provide cached or fallback explanations

### Requirement 7: Git Analysis Engine

**User Story:** As a developer, I want to understand code evolution through git history, so that I can learn from past decisions.

#### Acceptance Criteria

1. WHEN code is selected for storytelling, THE Git_Analysis_Engine SHALL retrieve commit history for the selected lines
2. THE Git_Analysis_Engine SHALL parse commit messages to extract architectural decisions and rationale
3. THE Git_Analysis_Engine SHALL identify code authors and change frequency patterns
4. WHEN multiple commits affect the same code, THE Git_Analysis_Engine SHALL construct a chronological narrative
5. THE Git_Analysis_Engine SHALL handle repositories with large histories efficiently without blocking the UI

### Requirement 8: Progress Dashboard

**User Story:** As a developer, I want to track my learning progress, so that I can see improvement over time.

#### Acceptance Criteria

1. THE Progress_Dashboard SHALL display time saved debugging as a cumulative metric
2. THE Progress_Dashboard SHALL display concepts mastered per week as a trend chart
3. THE Progress_Dashboard SHALL display mistake prediction accuracy as a percentage
4. WHEN a developer completes a learning challenge, THE Progress_Dashboard SHALL update the concepts mastered count
5. THE Progress_Dashboard SHALL be accessible via web browser and built with React and Tailwind CSS

### Requirement 9: Skill Level Assessment

**User Story:** As a developer, I want the system to understand my skill level, so that I receive appropriate feedback and challenges.

#### Acceptance Criteria

1. WHEN a developer first uses the system, THE CodeMentor_System SHALL perform an initial skill assessment
2. THE CodeMentor_System SHALL categorize developers as junior or mid-level based on code patterns and responses
3. WHEN skill level changes, THE CodeMentor_System SHALL adjust mistake predictions and challenge difficulty
4. THE CodeMentor_System SHALL continuously refine skill assessment based on developer interactions
5. THE CodeMentor_System SHALL allow developers to manually adjust their skill level if the assessment is incorrect

### Requirement 10: Data Persistence and Privacy

**User Story:** As a developer, I want my progress and code analysis to be saved securely, so that I can continue learning across sessions.

#### Acceptance Criteria

1. THE Backend_Service SHALL persist developer progress data across sessions
2. THE Backend_Service SHALL store skill assessments, completed challenges, and learning metrics
3. WHEN storing code context, THE Backend_Service SHALL anonymize or encrypt sensitive information
4. THE CodeMentor_System SHALL not transmit code to external services without developer consent
5. THE CodeMentor_System SHALL provide options to clear stored data and reset progress
