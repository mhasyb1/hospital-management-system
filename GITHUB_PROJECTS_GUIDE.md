# GitHub Projects Setup Guide

## Overview

This guide provides instructions for setting up and managing the Hospital Management System GitHub Projects board.

## Projects Board Structure

### Board Name: Hospital Management System - Development Board

### Columns

1. **📋 Backlog**
   - New tasks not yet prioritized
   - Feature requests
   - Enhancement suggestions

2. **📌 To Do**
   - Prioritized tasks ready to be worked on
   - Clear acceptance criteria
   - Assigned to team members

3. **🔄 In Progress**
   - Tasks currently being worked on
   - Linked to active branches
   - Regular updates in comments

4. **👀 In Review**
   - Tasks completed, awaiting review
   - Pull requests linked
   - Feedback from reviewers

5. **✅ Done**
   - Completed tasks
   - Tested and verified
   - Documentation updated

## Creating Issues

### Issue Categories

#### 1. Feature Issues
**Title Format:** `[FEATURE] Brief description`
**Labels:** `feature`, `enhancement`
**Priority:** High, Medium, Low

Example:
```
Title: [FEATURE] Implement Patient Registration System
Description: 
- Create patient registration form
- Validate input data
- Store in database
- Send confirmation email

Acceptance Criteria:
- Form accepts valid patient data
- Email confirmation sent
- Data stored correctly
```

#### 2. Bug Issues
**Title Format:** `[BUG] Brief description`
**Labels:** `bug`, `critical/major/minor`

Example:
```
Title: [BUG] Login page not responsive
Description: Login page layout breaks on mobile devices

Steps to Reproduce:
1. Open login page on mobile
2. Observe broken layout

Expected Behavior:
- Page should be fully responsive

Actual Behavior:
- Text overlaps, buttons misaligned
```

#### 3. Documentation Issues
**Title Format:** `[DOCS] Brief description`
**Labels:** `documentation`

Example:
```
Title: [DOCS] Create API Documentation
Description: Document all API endpoints with examples

Deliverables:
- List all endpoints
- Request/response examples
- Authentication requirements
- Error codes
```

#### 4. Task Issues
**Title Format:** `[TASK] Brief description`
**Labels:** `task`

Example:
```
Title: [TASK] Setup Development Environment
Description: Configure Node.js, MongoDB, and dependencies

Checklist:
- [ ] Install Node.js
- [ ] Install MongoDB
- [ ] Install dependencies
- [ ] Configure environment variables
- [ ] Test setup
```

## Issue Assignment

### Assignment Strategy

**Muhammad Haseeb (Project Manager):**
- Overall project management tasks
- Sprint planning
- Repository management
- Deployment coordination
- Risk management

**Mubarak Andarabi (Documentation & Design Lead):**
- System design documents
- Architecture diagrams
- API documentation
- UI/UX design
- Testing plans

**Shared Responsibilities:**
- Feature implementation (take turns)
- Code review
- Testing
- Documentation updates

## Workflow Process

### 1. Creating a Task
```
1. Click "Projects" tab
2. Click "New project" or select existing board
3. Add issue to backlog
4. Set priority and labels
5. Add to milestone if applicable
```

### 2. Moving to "To Do"
```
- Prioritize task
- Add detailed acceptance criteria
- Assign to team member
- Set due date
- Link related issues
```

### 3. Moving to "In Progress"
```
- Create feature branch
- Link pull request
- Update issue with progress
- Add comments for clarification
```

### 4. Moving to "In Review"
```
- Push code to GitHub
- Create pull request
- Request review from team
- Link PR to issue
- Update issue status
```

### 5. Moving to "Done"
```
- PR approved and merged
- Code tested and verified
- Documentation updated
- Close issue
- Archive/move to Done column
```

## Best Practices

### For Project Manager (Muhammad Haseeb)
1. ✓ Review all new issues within 24 hours
2. ✓ Keep board updated with task status
3. ✓ Schedule regular meetings
4. ✓ Monitor deadlines
5. ✓ Identify bottlenecks early
6. ✓ Update progress reports weekly

### For Documentation Lead (Mubarak Andarabi)
1. ✓ Document all decisions in issues
2. ✓ Create clear acceptance criteria
3. ✓ Maintain consistent naming
4. ✓ Update documentation with changes
5. ✓ Create architecture diagrams
6. ✓ Review documentation quality

### For Team
1. ✓ Assign yourself to issues before starting
2. ✓ Update issue status regularly
3. ✓ Comment on blockers immediately
4. ✓ Link PRs to related issues
5. ✓ Close completed issues promptly
6. ✓ Participate in reviews

## Milestone Planning

### Milestone 1: Project Setup (Week 1)
- [ ] Repository setup
- [ ] GitHub Projects setup
- [ ] Initial documentation
- [ ] Team role assignment

### Milestone 2: Requirements & Design (Week 2-3)
- [ ] Requirements documentation
- [ ] Architecture design
- [ ] Database schema
- [ ] UI mockups
- [ ] System diagrams

### Milestone 3: Backend Development (Week 4-7)
- [ ] API development
- [ ] Database implementation
- [ ] Authentication system
- [ ] Business logic

### Milestone 4: Frontend Development (Week 8-11)
- [ ] Frontend structure
- [ ] UI implementation
- [ ] API integration
- [ ] User testing

### Milestone 5: Testing & Launch (Week 12)
- [ ] Testing completion
- [ ] Bug fixes
- [ ] Deployment
- [ ] Final documentation

## Metrics & Tracking

### Key Metrics
- **Velocity:** Tasks completed per week
- **Burndown:** Remaining work over time
- **Lead Time:** Time from issue creation to completion
- **Cycle Time:** Time from "In Progress" to "Done"

### Reporting
- Weekly progress reports
- Monthly metrics review
- Sprint retrospectives
- Team performance tracking

## Tips for Success

1. **Keep issues small:** Aim for 2-3 hour tasks
2. **Be specific:** Clear acceptance criteria help
3. **Update regularly:** Don't let status get stale
4. **Communicate:** Comment on blockers immediately
5. **Review consistently:** Code review within 24 hours
6. **Document thoroughly:** Future reference is important
7. **Celebrate wins:** Acknowledge completed milestones

---

**Document Created:** June 1, 2026  
**Last Updated:** June 1, 2026  
**Maintained By:** Muhammad Haseeb & Mubarak Andarabi
