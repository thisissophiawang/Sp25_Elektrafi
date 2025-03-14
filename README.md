##  Capstone project - ElektraFi Gamification Features and Development Summary

 
![Workflow](https://github.com/thisissophiawang/Sp25_Elektrafi/blob/main/workflow.png)

## Main Features
### 1. Complete Streak Tracking System 


The system tracks consecutive task completions (streaks) across different timeframes (daily, weekly, monthly). It calculates current streak length, records the user's longest streak, and provides visual indicators of streak progress. The system also includes streak recovery options to prevent user discouragement from a single missed day.


### 2. Flinks API Integration for Task Verification 
Financial tasks are automatically verified through Flinks API integration, which connects to users' bank accounts to confirm actions like savings deposits or budget adherence. This provides objective verification rather than relying solely on self-reporting, enhancing the credibility of achievements.



### 3. Alternative Verification Mechanisms 


To address API instability issues, the system implements fallback verification options including delayed verification (checking account changes at a later time), pattern recognition of past financial behavior, and guided self-reporting with accountability features. This ensures users can continue engaging with the platform even when API connections are problematic.


### 4. Achievement and Reward System 

The platform features a comprehensive badge and medal system that rewards consistent financial behaviors. Users can earn bronze, silver, and gold medals based on streak length and task difficulty. Achievements are displayed in a dedicated gallery, and users receive notifications when unlocking new badges. The system integrates with the points economy to provide tangible rewards for accomplishments.


### 5. Enhanced User Interface and Feedback 

The interface provides immediate visual feedback for task completion, streak milestones, and badge unlocks. Animations celebrate achievements, progress bars visualize advancement toward goals, and a cohesive design ensures users understand their financial journey. The UI is fully responsive across all device sizes, maintaining a consistent experience.


### 6. Comprehensive Error Handling and Recovery 

The system implements robust error handling for API failures, network issues, and data synchronization problems. Users receive clear, non-technical explanations when problems occur, along with specific recovery actions. The application maintains local state during connectivity issues and provides synchronization when connections are restored, ensuring no progress is lost.



## Development Summary (Frontend)



![Frontend Data Flow](https://github.com/thisissophiawang/Sp25_Elektrafi/blob/main/frontend%20data%20flow.png)


### 1. First Commit - Foundation Building


The initial commit established the core architecture and data structures essential for the gamification system. It created the TypeScript type definitions, set up the React context for state management, implemented the basic task page UI, and integrated the navigation. This phase focused on creating a solid foundation with proper typing and component structure.


### 2. Second Commit - Data Integration 
The second commit integrated GraphQL for data management, replacing static data with dynamic API interactions. It implemented queries and mutations for task data, enhanced the context provider to work with server data, and improved the user interface with loading states and error handling. This phase connected the frontend to the backend, enabling persistent data and multi-device access.


### 3. Third Commit - Feature Completion 

The final commit completed the system with advanced features including the streak tracking system, badge and medal rewards, Flinks API integration, and comprehensive error handling. It expanded the type definitions, enhanced the context with verification strategies, implemented the achievement system, and polished the user interface. This phase transformed the basic task tracker into a fully-featured gamification platform that promotes financial wellness.


The development followed a phased implementation strategy, with each commit building upon the previous one and progressively enriching functionality and user experience. The entire process demonstrates the evolution from concept to a fully functional gamification system that effectively promotes financial wellness through engaging daily interactions.


## Development Summary (Backend)
![Backend Data Flow](https://github.com/thisissophiawang/Sp25_Elektrafi/blob/main/backend%20data%20flow.png)

The complete data flow for task completion:

1. User completes a task in the frontend → Frontend triggers `CompleteTask` GraphQL mutation (`src/graphql/query/tasks.mutations.ts`).
2. Backend `TaskResolver` (`src/modules/tasks/tasks.resolver.ts`) receives the request → Calls `TaskService.completeTask()`.
3. `TaskService` (`src/modules/tasks/tasks.service.ts`) calls `VerificationService` for validation → Updates task status and streak upon verification.
4. `TaskService` calls `RewardService` (`src/modules/rewards/rewards.service.ts`) for reward calculations → Updates user points and badges.
5. Backend returns updated task data → Frontend Apollo Client updates cache → UI reflects the new state.
6. If API failure occurs, alternative verification (`src/modules/verification/fallback/alternative-verification.ts`) is triggered → Records as self-reported verification → Still returns success but marks the verification type.


