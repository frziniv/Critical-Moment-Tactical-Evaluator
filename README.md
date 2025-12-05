# Critical-Moment-Tactical-Evaluator
// CriticalTactics.ts

/**
 * Defines a potential action for the agent to take in a critical moment.
 */
interface TacticalAction {
    name: string;
    riskFactor: number; // 0.1 (Low Risk) to 1.0 (High Risk)
    rankImpact: number; // Positive value for Rank 1 potential


        if (isAllInMode) {
            // In 'All-In' mode, ignore risk and maximize raw rank impact.
            currentScore = action.rankImpact;
        } else {
            // Standard mode: Use WPI = RankImpact * (1 - RiskFactor)
            currentScore = action.rankImpact * (1 - action.riskFactor);
        }
        
        if (currentScore > maxScore) {
            maxScore = currentScore;
            bestAction = action;
        }
    }
    
    console.log(`Mode: ${scoringMetric}`);
    return bestAction;
}

// Example Usage
const highChanceAction = evaluateBestAction(ALL_ACTIONS, 0.6); // Calculated Risk Mode
const lowChanceAction = evaluateBestAction(ALL_ACTIONS, 0.1);  // All-In Mode

console.log(`Recommended Action (High Win Chance): ${highChanceAction ? highChanceAction.name : "Wait"}`);
console.log(`Recommended Action (Low Win Chance): ${lowChanceAction ? lowChanceAction.name : "Wait"}`);recommendedAction ? recommendedAction.name : "Wait"}`);
