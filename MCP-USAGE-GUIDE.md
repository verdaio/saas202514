# Claude Code MCP Usage Guide

**Project Context:** Multi-tenant SaaS platform for Microsoft ecosystem (Excel, OneDrive, Azure)

---

## 🚀 Quick Reference

| Need | Use MCP | Example |
|------|---------|---------|
| **Security check** | Socket | "Is this package safe?" |
| **User behavior** | Clarity | "How do users engage with this?" |
| **Business data** | Excel/Graph | "What do the numbers say?" |
| **Code architecture** | Context7 | "Where is this implemented?" |
| **Competitor intel** | Apify | "What are competitors doing?" |
| **Design specs** | Figma | "What color should this be?" |
| **BI dashboards** | Tableau | "Show me this quarter's metrics" |
| **Cross-source data** | Coupler.io | "Compare data from X and Y" |
| **Local files** | Windows | "Read the config file" |

**Golden Rule:** If you can answer in 30 seconds without an MCP, just answer it.

---

## 📊 MCP Availability Status

| MCP | Status | Purpose | Last Checked |
|-----|--------|---------|--------------|
| Socket | ⚪ Unknown | Dependency security | Auto-detect on first use |
| Clarity | ⚪ Unknown | Web analytics | Auto-detect on first use |
| Excel/Graph | ⚪ Unknown | Business data | Auto-detect on first use |
| Context7 | ⚪ Unknown | Code understanding | Auto-detect on first use |
| Apify | ⚪ Unknown | Competitive intel | Auto-detect on first use |
| Figma | ⚪ Unknown | Design system | Auto-detect on first use |
| Tableau | ⚪ Unknown | BI dashboards | Auto-detect on first use |
| Coupler.io | ⚪ Unknown | Unified data hub | Auto-detect on first use |
| Windows | ⚪ Unknown | Local file system | Auto-detect on first use |

*Claude Code will auto-detect and update status on first attempted use*

---

## 🎯 Available MCPs & When to Use

### Socket MCP - Dependency Security Scanner

**Recognition Patterns (think about):**
- Adding or evaluating dependencies?
- Making package choices?
- Security concerns mentioned?

**Use For:**
- Non-trivial npm packages (skip for express, react, lodash - assume safe)
- Unfamiliar libraries
- Packages with similar alternatives (help choose)
- Security audits

**Skip For:**
- Core ecosystem packages (express, react, vue, next.js)
- Packages you've already vetted this session
- Simple tasks where security isn't the focus

---

### Microsoft Clarity MCP - Web Analytics

**Recognition Patterns:**
- User behavior or engagement questions?
- Data-driven product decisions?
- Performance or bounce rate analysis?

**Use For:**
- Feature adoption analysis
- Engagement metrics by segment
- Performance investigation
- A/B test validation

**Skip For:**
- Questions about design (use Figma)
- Questions about past data (use Excel historical)
- Real-time data when not critical

---

### Microsoft Graph / Excel MCP - Business Data Access

**Recognition Patterns:**
- References to spreadsheets or business data?
- Customer lists, metrics, financials?
- Historical business intelligence?

**Use For:**
- Customer data lookups
- Historical trends
- Business metrics
- CRM data access

**Skip For:**
- Real-time analytics (use Clarity)
- Competitive data (use Apify)
- When user can provide data faster

---

### Context7 MCP - Deep Code Understanding

**Recognition Patterns:**
- Architecture or structure questions?
- "Where is X?" or "How does Y work?"
- Refactoring or feature planning?

**Use For:**
- Understanding multi-tenant isolation
- Finding all occurrences of a pattern
- Architectural decisions
- Dependency mapping

**Skip For:**
- Simple file searches (use Windows MCP)
- Questions about single files (just read them)
- When you already know the answer

---

### Windows MCP - Local File System

**Recognition Patterns:**
- Need to access local files?
- Config, logs, or documentation?
- File searches?

**Use For:**
- Reading configuration files
- Searching project documentation
- Log file analysis
- Pattern-based file finding

**Skip For:**
- Code architecture questions (use Context7)
- When file path is already known (just read it)

---

### Apify MCP - Competitive Intelligence

**Recognition Patterns:**
- Competitor mentions?
- Market research questions?
- "What are others doing?"

**Use For:**
- Competitor feature comparison
- Pricing intelligence
- Market trend research
- Public data gathering

**⚠️ Slow - Use Sparingly:**
- Can take 30+ seconds per query
- Don't run in parallel with other MCPs
- Cache results aggressively

---

### Tableau MCP - Business Intelligence Dashboards

**Recognition Patterns:**
- BI metrics or dashboard questions?
- Strategic decisions needing data?
- Executive reports?

**Use For:**
- Tenant-level performance
- KPI trends
- Strategic metrics
- Board-ready insights

---

### Figma MCP - Design System Access

**Recognition Patterns:**
- Design tokens needed (colors, spacing)?
- Component specifications?
- "How should this look?"

**Use For:**
- Extracting design tokens
- Component specifications
- Verifying design-code sync

---

### Coupler.io MCP - Unified Data Hub

**Recognition Patterns:**
- Need data from multiple sources?
- Cross-referencing required?
- Comprehensive reports?

**Use For:**
- Combining Excel + Clarity + Tableau
- Customer 360 views
- Cross-platform analysis

**Performance Note:** Slower than individual MCPs - use when cross-source value is high

---

## 🎲 Decision Matrix

### Task: Adding New Dependencies

**Priority:**
1. **Known safe packages** (express, react, vue) → Skip Socket, just install
2. **Unfamiliar packages** → Socket MCP first
3. **Borderline scores** → Document reasoning, let user decide

### Task: Understanding User Behavior

**Priority:**
1. **Real-time behavior** → Clarity MCP
2. **Historical trends** → Excel MCP
3. **Strategic insights** → Tableau MCP
4. **Comprehensive view** → Coupler.io MCP (all sources)

### Task: Code Navigation/Refactoring

**Priority:**
1. **Architecture understanding** → Context7 MCP
2. **Specific files** → Windows MCP (faster)
3. **Simple lookups** → Just read the file (fastest)

### Task: Feature Planning

**Priority:**
1. **User demand** → Clarity MCP (behavior data)
2. **Customer requests** → Excel MCP (feedback logs)
3. **Competitor landscape** → Apify MCP (market research)
4. **Technical feasibility** → Context7 MCP (architecture review)

### When Multiple MCPs Apply

**Run in parallel** (fast):
- Socket + Context7 (security + architecture)
- Clarity + Excel (behavior + business data)

**Run sequentially** (one is slow):
- Apify first (slow), then others
- Coupler.io alone (already combines sources)

---

## ⚠️ When NOT to Use MCPs

### Don't Over-Engineer Simple Tasks

**Skip MCPs when:**
- ✅ You can answer in 30 seconds
- ✅ Question doesn't need data
- ✅ User provided all context needed
- ✅ It's a well-known package (express, react, etc.)
- ✅ Checking would slow down more than it helps

**Examples:**

❌ **Don't:** Check Socket for `express`
✅ **Do:** Just install it (it's safe)

❌ **Don't:** Query Clarity for "Should I use flexbox or grid?"
✅ **Do:** Answer based on use case (no data needed)

❌ **Don't:** Use Context7 to find a file you already know about
✅ **Do:** Just read it directly

### The 30-Second Rule

**Before using any MCP, ask:**
> "Can I confidently answer this in 30 seconds without MCP data?"

If yes → Answer directly
If no → MCP adds value

---

## 🔥 Multi-MCP Workflows

### Scenario: Feature Planning with Data
**Trigger:** "Should we build [feature]?"

**Workflow:**
1. **Clarity MCP** → Check if users are trying to do this (behavior patterns)
2. **Excel MCP** → Review customer requests and feedback data
3. **Apify MCP** → See what competitors offer
4. **Context7 MCP** → Assess technical feasibility in architecture

**Synthesize:** Data-driven recommendation with evidence from all sources

---

### Scenario: Security Audit
**Trigger:** "How secure is our project?"

**Workflow:**
1. **Socket MCP** → Scan dependencies for vulnerabilities
2. **Context7 MCP** → Review authentication/authorization code
3. **Windows MCP** → Check for exposed secrets in configs

**Deliver:** Security posture with actionable improvements

---

### Scenario: Performance Investigation
**Trigger:** "The app feels slow"

**Workflow:**
1. **Clarity MCP** → Check engagement time, scroll depth, bounce rates
2. **Context7 MCP** → Identify performance bottlenecks in code
3. **Excel MCP** → Review performance metrics over time

**Recommend:** Specific optimizations based on data

---

### Scenario: Customer Success Report
**Trigger:** "How is [customer/tenant] doing?"

**Workflow:**
1. **Clarity MCP** → Usage patterns and engagement metrics
2. **Excel MCP** → Customer-specific data and history
3. **Tableau MCP** → BI dashboard metrics for this customer
4. **Coupler.io MCP** → Unified view across all sources

**Deliver:** Comprehensive customer health report

---

## ⚡ Performance Considerations

### API Limits & Costs

| MCP | Speed | Rate Limits | Cost |
|-----|-------|-------------|------|
| Socket | Fast (<2s) | Generous | Free |
| Clarity | Fast (<3s) | 100 req/hr | Free tier |
| Excel/Graph | Medium (5-10s) | Varies | Microsoft 365 |
| Context7 | Fast (<2s) | Generous | Varies |
| Apify | **Slow (30-60s)** | Usage-based | Pay per run |
| Figma | Fast (<2s) | 1000 req/hr | Free tier |
| Tableau | Medium (5-10s) | Varies | Tableau license |
| Coupler.io | Medium (10-15s) | Usage-based | Varies |
| Windows | Very fast (<1s) | No limits | Free |

### Caching Strategy

**Cache aggressively:**
- **Socket scores** → 24 hours (security scores don't change often)
- **Figma tokens** → Until design update mentioned
- **Context7 architecture** → Until code changes

**Cache for session:**
- **Clarity metrics** → Until user asks for fresh data
- **Excel data** → Ask user if fresh data needed

**Don't cache:**
- **Apify** → Competitive intel changes frequently
- **Tableau dashboards** → Real-time BI data

### Performance Tips

1. **Batch related queries** - Don't make 3 separate Clarity calls; make one comprehensive call
2. **Parallel when possible** - Fast MCPs can run together
3. **Apify last** - It's slow; run everything else first
4. **Cache in conversation** - "I checked Socket 5 minutes ago; scores were good"

---

## 🤔 Conflict Resolution

### When Socket Flags Risk But Package Needed

**Approach:**
1. Explain the risk clearly (CVEs, maintenance status, supply chain score)
2. Suggest alternatives if any exist
3. Provide mitigation strategies (version pinning, security monitoring)
4. Let user decide with full context

**Example:**
> "Socket flags `old-package` with a medium security risk (outdated dependencies).
> Alternatives: `new-package` (same features, better scores) or `modern-lib` (more features).
> If we must use `old-package`: Pin to version 2.1.4 and monitor for updates. Your call?"

---

### When Data Sources Disagree

**Approach:**
1. Present both perspectives clearly
2. Note confidence levels/recency of each source
3. Recommend based on most reliable or recent source
4. Explain reasoning

**Example:**
> "Clarity shows 45% engagement (last 7 days), but Excel historical data shows 32% (last quarter).
> This suggests a recent improvement. I'd trust Clarity for current state - looks like the recent
> feature launch helped. Want to dig into what changed?"

---

### When Multiple MCPs Give Partial Answers

**Approach:**
1. Combine insights from all sources
2. Note where data is missing or unclear
3. Fill gaps with reasoning
4. Be transparent about confidence level

---

## ✅ Best Practices

### 1. Transparency
Always tell the user when using an MCP:

✅ "Let me check Socket for security scores..."
✅ "I'll query Clarity to see user engagement..."
✅ "Pulling that data from your Excel file..."

### 2. Context Awareness
Before using an MCP, consider:
- Is this data actually needed for the task?
- Would this query provide valuable insights?
- Is there a simpler way to answer this?

### 3. Efficiency
Don't over-query:
- Cache results when appropriate
- Batch related queries together
- Only fetch what's needed
- Skip when answer is obvious

### 4. Security
Always respect boundaries:
- Don't access files outside allowed paths
- Don't expose sensitive data unnecessarily
- Verify permissions before operations
- Explain security trade-offs clearly

### 5. User Experience
- Explain what you found and **why it matters**
- Provide **actionable insights**, not just data dumps
- **Connect MCP results back to the user's original question**
- If MCP fails, continue gracefully with available information

---

## 💬 Example Conversations

### Example 1: Adding a Package (With Socket Check)

**User:** "Add express to the project"

**Claude Code:** "Express is a well-known, battle-tested framework. I'll add it without a security check (it's universally trusted).

Running `npm install express`...

✅ Installed successfully!"

---

**User:** "Add `some-obscure-package` for PDF generation"

**Claude Code:** "Let me check the security of `some-obscure-package` first with Socket MCP...

**Socket Analysis:**
- Supply Chain: 45/100 ⚠️
- Quality: 62/100 ⚠️
- Maintenance: Last updated 2 years ago ⚠️
- Known CVE: 1 medium-severity vulnerability

**Recommendation:** This package has concerning signals. Alternatives:
- `puppeteer` (95/100 across the board, actively maintained)
- `pdfkit` (90/100, Node.js native, good maintenance)

Should I use one of these instead, or do you specifically need `some-obscure-package`?"

---

### Example 2: Feature Request Analysis

**User:** "Should we add dark mode?"

**Claude Code:** "Great question! Let me gather data to help us decide...

**Checking user behavior with Clarity MCP...**
- 34% of users visit during evening hours (6pm-midnight)
- Average engagement time drops 15% after 8pm ⚠️

**Checking customer requests in Excel MCP...**
- 23 customer requests for dark mode in last quarter
- Ranked #3 in feature requests 🔥

**Checking competitors with Apify MCP...**
- 7 out of 10 competitors offer dark mode
- Standard feature in modern SaaS products

**Checking technical feasibility with Context7 MCP...**
- CSS variables already in use (easy theme switching) ✅
- No major architectural blockers
- Estimated: 2-3 day implementation

---

**Recommendation:** ✅ **Yes, add dark mode.**

**Reasoning:**
- Strong user need (34% evening usage, engagement drops)
- High customer demand (#3 requested feature)
- Competitive standard (70% of competitors have it)
- Technically straightforward (2-3 days)
- **Expected impact:** Improve evening engagement 10-15%"

---

### Example 3: Security Audit

**User:** "Is our project secure?"

**Claude Code:** "Let me run a comprehensive security audit...

**Checking dependencies with Socket MCP...**
- ⚠️ Found 2 packages with medium-risk vulnerabilities
- ⚠️ 1 outdated package with available security patch
- **Action needed:** Update `lodash` to patch CVE-2024-XXXX (high priority)

**Reviewing authentication code with Context7 MCP...**
- ✅ Multi-tenant isolation properly implemented
- ✅ JWT tokens with appropriate expiration (15 min access, 7 day refresh)
- ✅ Password hashing uses bcrypt with proper salt rounds

**Checking configuration files with Windows MCP...**
- ✅ No secrets in committed files
- ✅ `.env` properly gitignored
- ✅ API keys using environment variables
- ⚠️ CORS configuration is `'*'` (too permissive for production)

---

**Overall Security Posture:** 🟡 **Good** (7/10)

**Action Items:**
1. 🔴 **High Priority:** Update `lodash` to patch vulnerability
2. 🟠 **Medium Priority:** Restrict CORS to specific domains for production
3. 🟢 **Nice-to-have:** Consider adding rate limiting to API endpoints

Want me to fix #1 and #2 now?"

---

## 🎯 Proactive MCP Usage Patterns

Claude Code should **proactively suggest** using MCPs when:

### Security Context
- 💭 About to run `npm install` → "Let me check Socket first..."
- 💭 User mentions unfamiliar package → "Should I verify this package's security?"
- 💭 Discussing dependencies → "Want me to audit current dependencies?"

### Data Context
- 💭 User mentions metrics/analytics → "I can pull that from Clarity..."
- 💭 References Excel/customer data → "Let me query that file for you..."
- 💭 Asks about trends → "I can check our BI dashboards..."

### Code Context
- 💭 Asking about architecture → "Let me query the codebase with Context7..."
- 💭 Looking for files → "I'll use Windows MCP to search..."
- 💭 Refactoring discussion → "I can map the dependencies with Context7..."

### Competitive Context
- 💭 Mentions competitors → "I can gather current competitive data..."
- 💭 Market research question → "Let me check what's publicly available..."
- 💭 Feature comparison → "I'll pull competitor information with Apify..."

**Key principle:** Suggest MCPs proactively, but don't block simple tasks waiting for data.

---

## 🔧 Error Handling & Fallbacks

### If MCP Unavailable

| MCP | Fallback Strategy |
|-----|-------------------|
| **Socket** | Warn user, suggest manual security check at npmjs.com |
| **Clarity** | Offer to check alternative analytics or proceed without data |
| **Excel/Graph** | Ask user to manually provide data or skip data-dependent steps |
| **Context7** | Fall back to Windows MCP for file search, or manual navigation |
| **Apify** | Skip competitive intel or ask user for manual research |
| **Figma** | Ask for design specs manually or use best practices |
| **Tableau** | Use Excel for historical data or skip BI insights |
| **Coupler.io** | Query individual MCPs separately |
| **Windows** | Ask user for file contents manually |

### If Data Not Found

**Don't block progress:**
1. Explain what was searched and where
2. Suggest alternatives (different data source, manual input, reasonable assumptions)
3. Ask user how to proceed
4. Continue with best available information

**Example:**
> "I checked Clarity for engagement metrics but couldn't find data for that specific feature (might not be instrumented yet).
> I can: (1) proceed with overall engagement metrics, (2) you provide the data manually, or (3) we make reasonable assumptions. What works?"

### If Permissions Denied

1. Explain what permission is needed and why
2. Provide instructions for granting access (or point to docs)
3. Offer workaround if possible
4. Don't block - ask user how to proceed

---

## 📈 Continuous Improvement

### As You Use These MCPs

**Track patterns:**
- Which MCP combinations are most valuable?
- Which queries waste time?
- Where do MCPs conflict most often?

**Suggest improvements:**
- Gaps in data coverage → Suggest new MCP integrations
- Repeated queries → Suggest caching or preprocessing
- Slow workflows → Suggest optimization

**Update this guide:**
- Document new patterns discovered
- Add new example conversations
- Refine recognition patterns based on actual usage

---

## 📚 Notes for Claude Code

### When Reading This Guide

**Core principles:**
- Use MCPs **proactively** when they add clear value
- Always **explain what you're doing and why**
- **Connect MCP results back** to user's question
- Don't over-engineer simple tasks
- **Respect user's time** - be efficient

### When Uncertain

**Ask the user:**
- "Would you like me to check [MCP] for additional context?"
- "I can pull data from [sources] - which would be most valuable?"
- "This will take ~30 seconds - want me to check [MCP] or proceed without that data?"

### When MCPs Conflict

**Present all perspectives:**
1. Show conflicting data clearly
2. Explain possible reasons for discrepancy
3. Note which source is more reliable/recent
4. Make a recommendation with reasoning
5. Let user make final decision

---

**Last Updated:** Auto-update on each use
**Maintained By:** Claude Code + Development Team

---

## Summary

This guide helps Claude Code:
1. **Choose the right MCP** for each task (Quick Reference)
2. **Know when NOT to use MCPs** (avoid over-engineering)
3. **Orchestrate multiple MCPs** for complex questions (Multi-MCP Workflows)
4. **Handle conflicts and errors** gracefully (Conflict Resolution)
5. **Provide transparent, actionable insights** (Best Practices)

**Golden Rule:** MCPs are tools to provide better answers, not requirements. Use judgment. If you can answer well in 30 seconds without an MCP, just answer it.

---

This is a **living document**. Update it as you learn what works and what doesn't. The best MCP usage guide is the one that reflects real-world experience.
