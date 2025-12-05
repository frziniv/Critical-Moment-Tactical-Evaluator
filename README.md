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
    { name: "Initiate_Final_Attack", riskFactor: 0.8, rankImpact: 900 }, // High risk, high reward
    { name: "Prioritize_Defensive_Posturing", riskFactor: 0.2, rankImpact: 200 }, // Low risk, low impact
    { name: "Secure_Minor_Objective", riskFactor: 0.5, rankImpact: 400 }, // Moderate option
    { name: "Use_Ultimate_Ability", riskFactor: 0.6, rankImpact: 750 }
];

/**
 * Evaluates the best action based on Win Probability Impact (WPI) formula.
 * Formula: WPI = RankImpact * (1 - RiskFactor)
 * This favors high-impact actions where risk is manageable.
 * @param {TacticalAction[]} actions - Array of possible actions.
 * @returns {TacticalAction | null} The recommended action.
 */
function evaluateBestAction(actions: TacticalAction[]): TacticalAction | null {
    let bestAction: TacticalAction | null = null;
    let maxWPI = -Infinity;

    for (const action of actions) {
        // Calculate WPI: A higher score means a better calculated risk.
        const wpi = action.rankImpact * (1 - action.riskFactor);
        
        if (wpi > maxWPI) {
            maxWPI = wpi;
            bestAction = action;
        }
    }

    return bestAction;
}

// Example Usage
const recommendedAction = evaluateBestAction(ALL_ACTIONS);
console.log(`Recommended Action in Critical Moment: ${recommendedAction ? recommendedAction.name : "Wait"}`);
