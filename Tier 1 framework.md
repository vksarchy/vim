this is the .jsx file code: 

import { useState } from "react";

const PILLARS = [
  {
    id: "identity",
    symbol: "I",
    title: "Identity Before Action",
    subtitle: "They are before they do",
    gap: "You act from motivation. They act from identity.",
    explanation:
      "Tier-1 people don't wait to feel motivated. They've decided who they are — and that decision removes the question of whether to act. An entrepreneur who has decided 'I am someone who calls five leads before noon' doesn't negotiate with himself at 9am. You're still negotiating. The rewire: stop asking 'should I do this?' Start asking 'is this what someone like me does?'",
    daily: [
      "Write one sentence: 'I am someone who ___.' Make it behavioral, not aspirational.",
      "When you catch yourself hesitating, ask: would the person I'm becoming hesitate here?",
      "At night: did I act like that person today? One yes or no. No elaboration.",
    ],
    anchor: "Identity is the decision that ends all smaller decisions.",
  },
  {
    id: "stakes",
    symbol: "S",
    title: "Manufactured Stakes",
    subtitle: "They make losing real",
    gap: "You have diffuse fear. They have specific, dated, social stakes.",
    explanation:
      "Tier-1 people don't have more courage — they've engineered situations where retreat is more painful than advance. They make public commitments, take on investors, tell people they respect what they'll deliver. They manufacture the very pressure that forces action. You've been keeping your ambitions private, which means failure has no social cost. Invisible stakes produce invisible effort.",
    daily: [
      "One public commitment per week — to someone whose opinion you care about. Specific and dated.",
      "Write your 'May 2027 nightmare' and read it once a week. Keep the avoidance system warm.",
      "Before any important task: name what you lose if you don't do it today. Not eventually. Today.",
    ],
    anchor: "Make the cost of inaction more visible than the discomfort of action.",
  },
  {
    id: "discharge",
    symbol: "D",
    title: "No Discharge Valve",
    subtitle: "They don't release pressure through fantasy",
    gap: "You medicate desire with imagination. They let pressure build until it forces action.",
    explanation:
      "Every time you fantasize about the outcome — the speech, the lifestyle, the recognition — you discharge the exact energy that should be driving you to move. Your brain registers a micro-dose of reward without the work. The pressure bleeds out. Inertia returns. Tier-1 people don't do this. They've learned — often through failure — that imagination is debt, not currency. You don't get to feel the feeling until you've earned it.",
    daily: [
      "Catch the fantasy loop. When it starts, stop. Write one action you can take in the next hour instead.",
      "Rule: no imagining the outcome until you've done one real thing toward it today.",
      "Replace the fantasy with a question: 'What's the next physical action?' Then do it.",
    ],
    anchor: "Pressure that doesn't discharge becomes motion.",
  },
  {
    id: "mornings",
    symbol: "M",
    title: "Morning as Conquest",
    subtitle: "They own the first hour",
    gap: "You drift into the day. They attack it.",
    explanation:
      "The first 60-90 minutes of your day set the neurological tone for everything that follows. Tier-1 people treat the morning as a beachhead — the first territory to be taken. Not to optimize, not to grind — but to establish that today is not passive. One hard thing before the world demands anything of you. This rewires the self-image from 'reactive person' to 'person who initiates.' It compounds over 90 days into a different identity.",
    daily: [
      "One hard action before 10am. Not planning. Not reading. A real outward move — call, visit, message sent.",
      "No social media, no news, no content consumption before the hard action is done.",
      "Name the hard action the night before. Remove the morning decision entirely.",
    ],
    anchor: "Win the morning and the day already belongs to you.",
  },
  {
    id: "feedback",
    symbol: "F",
    title: "Reality as Teacher",
    subtitle: "They close loops. You leave them open.",
    gap: "You plan and imagine. They act, get feedback, and adjust.",
    explanation:
      "Tier-1 people are in constant contact with reality. They send the proposal and find out it was wrong. They make the call and hear the objection. They run the number and see it doesn't work. Then they adjust. You've been staying in the planning phase because planning feels like progress without the risk of real feedback. But without feedback loops, you're flying blind and calling it strategy. Reality is not your enemy. It's your fastest teacher.",
    daily: [
      "One closed loop per day minimum. Something sent, called, visited, submitted — that gets a real response.",
      "Weekly: what did reality tell me this week that my plan didn't anticipate?",
      "Track rejections, not just wins. Rejections mean you're in contact with the world.",
    ],
    anchor: "The map improves only when you compare it to the terrain.",
  },
  {
    id: "anava",
    symbol: "A",
    title: "Name the Anava",
    subtitle: "Your tradition already has the diagnosis",
    gap: "You experience contraction as default. They've built systems to fight it.",
    explanation:
      "Anava malam — the primary bond in Shaiva Siddhantam — is the sense of smallness, the contracted self that says 'I am limited, I cannot, I am not enough.' Every time you defer, distract, or fantasize — that is anava malam operating. Not weakness. Not laziness. The primary spiritual obstacle your tradition has named for thousands of years. Tier-1 people in your framework aren't free of anava — they've just built habits that override it before it settles. You need the same.",
    daily: [
      "When inertia hits: say aloud or in writing — 'this is anava malam.' Name it. Then move.",
      "Your Shaiva practice is not separate from your work. Each act of overcoming contraction is sadhana.",
      "Weekly: one reading from Thiruvaasagam. Not for comfort — for the fire Manikkavasagar had.",
    ],
    anchor: "Nataraja dances through destruction. He does not wait for conditions to improve.",
  },
];

const WEEKLY_REVIEW = [
  "How many public commitments did I make this week?",
  "How many real closed loops — actual responses from reality?",
  "Did I discharge pressure through fantasy instead of action? When?",
  "Did I win the morning 5 out of 7 days?",
  "One moment I acted like the person I'm becoming.",
  "One moment anava malam won. What triggered it?",
  "What does next week's version of me do differently?",
];

export default function Tier1Framework() {
  const [active, setActive] = useState(null);
  const [checked, setChecked] = useState({});
  const [reviewOpen, setReviewOpen] = useState(false);

  const toggleCheck = (pillarId, idx) => {
    const key = `${pillarId}-${idx}`;
    setChecked((prev) => ({ ...prev, [key]: !prev[key] }));
  };

  const activePillar = PILLARS.find((p) => p.id === active);

  return (
    <div style={{
      minHeight: "100vh",
      background: "#0a0a0a",
      color: "#e8e0d0",
      fontFamily: "'Georgia', 'Times New Roman', serif",
      padding: "0",
      overflowX: "hidden",
    }}>
      {/* Header */}
      <div style={{
        borderBottom: "1px solid #2a2a2a",
        padding: "2.5rem 2rem 2rem",
        position: "relative",
        overflow: "hidden",
      }}>
        <div style={{
          position: "absolute",
          top: 0, left: 0, right: 0, bottom: 0,
          background: "radial-gradient(ellipse at 20% 50%, rgba(180,120,40,0.06) 0%, transparent 60%)",
          pointerEvents: "none",
        }} />
        <div style={{ maxWidth: 720, margin: "0 auto", position: "relative" }}>
          <div style={{
            fontSize: "0.65rem",
            letterSpacing: "0.25em",
            color: "#6b5a3a",
            textTransform: "uppercase",
            marginBottom: "0.75rem",
            fontFamily: "monospace",
          }}>
            Rewiring Protocol — Personal OS
          </div>
          <h1 style={{
            fontSize: "clamp(1.8rem, 5vw, 2.8rem)",
            fontWeight: "normal",
            margin: 0,
            lineHeight: 1.15,
            color: "#f0e8d8",
            letterSpacing: "-0.02em",
          }}>
            The Tier-1 Framework
          </h1>
          <p style={{
            color: "#6b5a3a",
            marginTop: "0.75rem",
            fontSize: "0.95rem",
            fontStyle: "italic",
            lineHeight: 1.6,
          }}>
            Six pillars. Daily practice. 90 days to a different identity.
          </p>
        </div>
      </div>

      {/* Gap Statement */}
      <div style={{
        maxWidth: 720,
        margin: "2rem auto",
        padding: "0 2rem",
      }}>
        <div style={{
          background: "#111",
          border: "1px solid #2a2a2a",
          borderLeft: "3px solid #8b6914",
          padding: "1.25rem 1.5rem",
          fontSize: "0.9rem",
          lineHeight: 1.7,
          color: "#a09070",
        }}>
          Tier-1 people are not more talented. They are not more disciplined by nature. They have built
          specific structures — identity, stakes, feedback, morning rituals — that make action the path
          of least resistance. You have not built those structures yet. That is the entire gap.
          It is closeable.
        </div>
      </div>

      {/* Pillars Grid */}
      <div style={{
        maxWidth: 720,
        margin: "0 auto",
        padding: "0 2rem 2rem",
      }}>
        <div style={{
          fontSize: "0.65rem",
          letterSpacing: "0.2em",
          color: "#4a3a22",
          textTransform: "uppercase",
          fontFamily: "monospace",
          marginBottom: "1rem",
        }}>
          Six Pillars — tap to expand
        </div>

        {PILLARS.map((pillar, i) => (
          <div
            key={pillar.id}
            onClick={() => setActive(active === pillar.id ? null : pillar.id)}
            style={{
              marginBottom: "0.5rem",
              border: `1px solid ${active === pillar.id ? "#8b6914" : "#1e1e1e"}`,
              background: active === pillar.id ? "#111" : "#0d0d0d",
              cursor: "pointer",
              transition: "all 0.2s ease",
            }}
          >
            {/* Pillar Header */}
            <div style={{
              display: "flex",
              alignItems: "center",
              gap: "1rem",
              padding: "1rem 1.25rem",
            }}>
              <div style={{
                width: 36,
                height: 36,
                background: active === pillar.id ? "#8b6914" : "#1a1a1a",
                color: active === pillar.id ? "#0a0a0a" : "#4a3a22",
                display: "flex",
                alignItems: "center",
                justifyContent: "center",
                fontFamily: "monospace",
                fontSize: "0.85rem",
                fontWeight: "bold",
                flexShrink: 0,
                transition: "all 0.2s",
              }}>
                {pillar.symbol}
              </div>
              <div style={{ flex: 1 }}>
                <div style={{
                  fontSize: "1rem",
                  color: active === pillar.id ? "#f0e8d8" : "#c8b898",
                  marginBottom: "0.15rem",
                }}>
                  {pillar.title}
                </div>
                <div style={{
                  fontSize: "0.75rem",
                  color: "#4a3a22",
                  fontStyle: "italic",
                }}>
                  {pillar.subtitle}
                </div>
              </div>
              <div style={{
                color: "#4a3a22",
                fontSize: "1rem",
                transform: active === pillar.id ? "rotate(180deg)" : "none",
                transition: "transform 0.2s",
              }}>
                ▾
              </div>
            </div>

            {/* Expanded Content */}
            {active === pillar.id && (
              <div style={{ borderTop: "1px solid #1e1e1e" }}>
                {/* Gap */}
                <div style={{
                  padding: "1rem 1.25rem 0.75rem",
                  background: "#0f0f0f",
                  fontSize: "0.8rem",
                  color: "#8b6914",
                  fontFamily: "monospace",
                  letterSpacing: "0.05em",
                }}>
                  ↳ {pillar.gap}
                </div>

                {/* Explanation */}
                <div style={{
                  padding: "1.25rem 1.25rem 0",
                  fontSize: "0.88rem",
                  lineHeight: 1.75,
                  color: "#9a8a70",
                }}>
                  {pillar.explanation}
                </div>

                {/* Daily Practices */}
                <div style={{ padding: "1.25rem 1.25rem 0" }}>
                  <div style={{
                    fontSize: "0.65rem",
                    letterSpacing: "0.2em",
                    color: "#4a3a22",
                    textTransform: "uppercase",
                    fontFamily: "monospace",
                    marginBottom: "0.75rem",
                  }}>
                    Daily Practice
                  </div>
                  {pillar.daily.map((item, idx) => {
                    const key = `${pillar.id}-${idx}`;
                    return (
                      <div
                        key={idx}
                        onClick={(e) => { e.stopPropagation(); toggleCheck(pillar.id, idx); }}
                        style={{
                          display: "flex",
                          gap: "0.75rem",
                          marginBottom: "0.6rem",
                          cursor: "pointer",
                          alignItems: "flex-start",
                        }}
                      >
                        <div style={{
                          width: 16,
                          height: 16,
                          border: `1px solid ${checked[key] ? "#8b6914" : "#2a2a2a"}`,
                          background: checked[key] ? "#8b6914" : "transparent",
                          flexShrink: 0,
                          marginTop: "0.15rem",
                          display: "flex",
                          alignItems: "center",
                          justifyContent: "center",
                          fontSize: "0.6rem",
                          color: "#0a0a0a",
                          transition: "all 0.15s",
                        }}>
                          {checked[key] ? "✓" : ""}
                        </div>
                        <div style={{
                          fontSize: "0.85rem",
                          lineHeight: 1.6,
                          color: checked[key] ? "#4a3a22" : "#8a7a60",
                          textDecoration: checked[key] ? "line-through" : "none",
                          transition: "all 0.15s",
                        }}>
                          {item}
                        </div>
                      </div>
                    );
                  })}
                </div>

                {/* Anchor */}
                <div style={{
                  margin: "1.25rem 1.25rem 1.25rem",
                  padding: "0.875rem 1rem",
                  borderLeft: "2px solid #8b6914",
                  background: "#0a0a0a",
                  fontSize: "0.83rem",
                  fontStyle: "italic",
                  color: "#c8a84a",
                  lineHeight: 1.6,
                }}>
                  "{pillar.anchor}"
                </div>
              </div>
            )}
          </div>
        ))}
      </div>

      {/* What They're Doing That You're Not */}
      <div style={{
        maxWidth: 720,
        margin: "0 auto",
        padding: "0 2rem 2rem",
      }}>
        <div style={{
          fontSize: "0.65rem",
          letterSpacing: "0.2em",
          color: "#4a3a22",
          textTransform: "uppercase",
          fontFamily: "monospace",
          marginBottom: "1rem",
        }}>
          The Actual Gap — What They Do That You Don't
        </div>

        {[
          ["They tell people what they'll deliver", "You keep ambitions private to avoid accountability"],
          ["They talk to reality every day", "You stay in planning mode to avoid rejection"],
          ["They track what they actually did", "You track what you intend to do"],
          ["They let discomfort be the signal to move", "You let discomfort be the signal to retreat"],
          ["They have one philosophical anchor", "You sample many and commit to none"],
          ["They close the day with an honest review", "You close the day with content consumption"],
          ["They act before they feel ready", "You wait for readiness that never fully arrives"],
        ].map(([them, you], i) => (
          <div key={i} style={{
            display: "grid",
            gridTemplateColumns: "1fr 1fr",
            gap: "1px",
            marginBottom: "1px",
            background: "#1a1a1a",
          }}>
            <div style={{
              padding: "0.875rem 1rem",
              background: "#0d0d0d",
              fontSize: "0.82rem",
              lineHeight: 1.5,
              color: "#8a7a60",
              borderLeft: "2px solid #1e3a1e",
            }}>
              <span style={{ color: "#3a6a3a", fontSize: "0.65rem", display: "block", marginBottom: "0.25rem", fontFamily: "monospace" }}>TIER-1</span>
              {them}
            </div>
            <div style={{
              padding: "0.875rem 1rem",
              background: "#0d0d0d",
              fontSize: "0.82rem",
              lineHeight: 1.5,
              color: "#8a7a60",
              borderLeft: "2px solid #3a1e1e",
            }}>
              <span style={{ color: "#6a3a3a", fontSize: "0.65rem", display: "block", marginBottom: "0.25rem", fontFamily: "monospace" }}>CURRENT</span>
              {you}
            </div>
          </div>
        ))}
      </div>

      {/* Weekly Review */}
      <div style={{
        maxWidth: 720,
        margin: "0 auto",
        padding: "0 2rem 3rem",
      }}>
        <div
          onClick={() => setReviewOpen(!reviewOpen)}
          style={{
            border: "1px solid #1e1e1e",
            background: "#0d0d0d",
            padding: "1rem 1.25rem",
            cursor: "pointer",
            display: "flex",
            justifyContent: "space-between",
            alignItems: "center",
          }}
        >
          <div>
            <div style={{
              fontSize: "0.65rem",
              letterSpacing: "0.2em",
              color: "#4a3a22",
              textTransform: "uppercase",
              fontFamily: "monospace",
              marginBottom: "0.25rem",
            }}>
              Weekly Ritual
            </div>
            <div style={{ fontSize: "0.95rem", color: "#c8b898" }}>Sunday Review Questions</div>
          </div>
          <div style={{
            color: "#4a3a22",
            transform: reviewOpen ? "rotate(180deg)" : "none",
            transition: "transform 0.2s",
          }}>▾</div>
        </div>

        {reviewOpen && (
          <div style={{
            border: "1px solid #1e1e1e",
            borderTop: "none",
            background: "#090909",
          }}>
            {WEEKLY_REVIEW.map((q, i) => (
              <div key={i} style={{
                padding: "0.875rem 1.25rem",
                borderBottom: i < WEEKLY_REVIEW.length - 1 ? "1px solid #141414" : "none",
                display: "flex",
                gap: "1rem",
                alignItems: "flex-start",
              }}>
                <div style={{
                  color: "#4a3a22",
                  fontFamily: "monospace",
                  fontSize: "0.75rem",
                  flexShrink: 0,
                  marginTop: "0.15rem",
                }}>
                  {String(i + 1).padStart(2, "0")}
                </div>
                <div style={{
                  fontSize: "0.85rem",
                  lineHeight: 1.6,
                  color: "#8a7a60",
                }}>
                  {q}
                </div>
              </div>
            ))}
          </div>
        )}

        {/* Footer */}
        <div style={{
          marginTop: "2rem",
          padding: "1.25rem",
          background: "#080808",
          border: "1px solid #1a1a1a",
          textAlign: "center",
        }}>
          <div style={{
            fontSize: "0.75rem",
            color: "#4a3a22",
            fontStyle: "italic",
            lineHeight: 1.8,
          }}>
            Nataraja dances through destruction. He does not wait for conditions to improve.<br />
            <span style={{ color: "#2a1a0a" }}>— Shaiva anchor for the 90-day sprint</span>
          </div>
        </div>
      </div>
    </div>
  );
}
