# Critical-Moment-Tactical-Evaluator
// CriticalTactics.ts

/**
 * Defines a potential action for the agent to take in a critical moment.
 */
interface TacticalAction {
    name: string;
    riskFactor: number; // 0.1 (Low Risk) to 1.0 (High Risk)
    rankImpact: number; // Positive value for Rank 1 potential
}

const ALL_ACTIONS: TacticalAction[] = [
    { name: "Initiate_Final_Attack", riskFactor: 0.8, rankImpact: 900 },
    { name: "Prioritize_Defensive_Posturing", riskFactor: 0.2, rankImpact: 200 },
    { name: "Secure_Minor_Objective", riskFactor: 0.5, rankImpact: 400 },
    { name: "Use_Ultimate_Ability", riskFactor: 0.6, rankImpact: 750 },
    { name: "Execute_Desperate_Flank", riskFactor: 0.95, rankImpact: 950 } // Extremely high risk, slightly higher reward
];

const CRITICAL_WIN_CHANCE_THRESHOLD = 0.3; // If win chance is below 30%, go 'All-In'.

/**
 * Evaluates the best action based on Win Probability Impact (WPI) or 'All-In' mode.
 * @param {TacticalAction[]} actions - Array of possible actions.
 * @param {number} currentWinChance - The agent's current estimated chance of achieving Rank 1 (0.0 to 1.0).
 * @returns {TacticalAction | null} The recommended action.
 */
function evaluateBestAction(actions: TacticalAction[], currentWinChance: number): TacticalAction | null {
    let bestAction: TacticalAction | null = null;
    let maxScore = -Infinity;
    
    // NEW EDIT: Check for 'All-In' Mode
    const isAllInMode = currentWinChance < CRITICAL_WIN_CHANCE_THRESHOLD;
    const scoringMetric = isAllInMode ? "Rank Impact (All-In)" : "WPI (Calculated Risk)";
    
    for (const action of actions) {
        let currentScore: number;

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
