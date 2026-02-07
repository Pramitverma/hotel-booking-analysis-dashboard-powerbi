# Contributing to Hotel Booking Demand Analysis Dashboard

First off, thank you for considering contributing to this project! 🎉

The following is a set of guidelines for contributing to the Hotel Booking Demand Analysis Dashboard. These are mostly guidelines, not rules. Use your best judgment, and feel free to propose changes to this document in a pull request.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
  - [Reporting Bugs](#reporting-bugs)
  - [Suggesting Enhancements](#suggesting-enhancements)
  - [Code Contributions](#code-contributions)
- [Development Setup](#development-setup)
- [Style Guidelines](#style-guidelines)
- [Commit Message Guidelines](#commit-message-guidelines)
- [Pull Request Process](#pull-request-process)

---

## 🤝 Code of Conduct

This project and everyone participating in it is governed by our commitment to creating a welcoming and inclusive environment. By participating, you are expected to uphold this code:

- **Be Respectful**: Treat everyone with respect and kindness
- **Be Collaborative**: Work together and help each other
- **Be Professional**: Keep discussions focused on the project
- **Be Patient**: Remember that everyone is learning

---

## 🚀 How Can I Contribute?

### 🐛 Reporting Bugs

Before creating bug reports, please check existing issues to avoid duplicates.

**When submitting a bug report, include:**

- **Clear title and description** of the issue
- **Steps to reproduce** the problem
- **Expected behavior** vs **actual behavior**
- **Screenshots** if applicable
- **Environment details**:
  - Power BI Desktop version
  - Operating System
  - Dataset size/version

**Example Bug Report:**

```markdown
**Title:** Cancellation Rate calculation incorrect for April

**Description:** 
The cancellation rate for April shows 40.80% but manual calculation 
shows it should be 38.50%.

**Steps to Reproduce:**
1. Open Hotel_Booking_Analysis.pbix
2. Navigate to Cancellation Trends page
3. Check April bar chart value

**Expected:** 38.50%
**Actual:** 40.80%

**Environment:**
- Power BI Desktop: Version 2.125
- OS: Windows 11
- Dataset: hotel_bookings.xlsx (119,390 rows)
```

### 💡 Suggesting Enhancements

We love to receive enhancement suggestions! Here's how to submit them:

**Enhancement Suggestion Template:**

```markdown
**Feature Request:** Add predictive cancellation model

**Problem it solves:** 
Currently we can only see historical cancellations. A predictive 
model would help hotels proactively manage at-risk bookings.

**Proposed Solution:**
Integrate Python script using scikit-learn to predict cancellation 
probability based on lead time, deposit type, and previous cancellations.

**Alternatives Considered:**
- DAX-based scoring (limited functionality)
- R integration (fewer users familiar with R)

**Additional Context:**
This would align with the "Future Enhancements" roadmap.
```

### 💻 Code Contributions

**Types of contributions we're looking for:**

- 🐛 Bug fixes
- ✨ New features from roadmap
- 📊 New visualizations
- 📝 Documentation improvements
- 🎨 Dashboard design enhancements
- 🔧 Performance optimizations
- 🧪 Data quality improvements

---

## 🛠️ Development Setup

### Prerequisites

```
✅ Power BI Desktop (latest version)
✅ Git installed
✅ GitHub account
✅ Basic understanding of DAX and Power Query
```

### Setup Instructions

1. **Fork the repository**
   ```bash
   # Click "Fork" button on GitHub
   ```

2. **Clone your fork**
   ```bash
   git clone https://github.com/YOUR-USERNAME/hotel-booking-demand-analysis.git
   cd hotel-booking-demand-analysis
   ```

3. **Create a branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/bug-description
   ```

4. **Open Power BI file**
   ```
   Open Dashboard/Hotel_Booking_Analysis.pbix in Power BI Desktop
   ```

5. **Make your changes**
   - Edit visualizations, DAX measures, or Power Query steps
   - Test thoroughly with the full dataset
   - Document any new measures in DAX_Formulas.md

6. **Save and commit**
   ```bash
   git add .
   git commit -m "feat: add predictive cancellation score"
   ```

7. **Push to your fork**
   ```bash
   git push origin feature/your-feature-name
   ```

8. **Create Pull Request**
   - Go to original repository on GitHub
   - Click "New Pull Request"
   - Select your branch
   - Fill in PR template

---

## 📐 Style Guidelines

### Power BI Best Practices

**Naming Conventions:**

```dax
// ✅ GOOD - Clear, descriptive names
Total Bookings = COUNT(Bookings[booking_id])
Cancellation Rate % = DIVIDE([Cancelled Bookings], [Total Bookings], 0) * 100

// ❌ BAD - Vague, unclear names
Measure1 = COUNT(Bookings[booking_id])
CR = DIVIDE([CB], [TB], 0) * 100
```

**DAX Formatting:**

```dax
// ✅ GOOD - Well formatted with line breaks
Revenue Lost to Cancellations = 
SUMX(
    FILTER(
        Bookings,
        Bookings[is_canceled] = TRUE
    ),
    Bookings[adr] * Bookings[total_nights]
)

// ❌ BAD - Single line, hard to read
Revenue Lost = SUMX(FILTER(Bookings,Bookings[is_canceled]=TRUE),Bookings[adr]*Bookings[total_nights])
```

**Visual Design:**

- ✅ Use consistent color scheme (Blues for primary, Red for alerts)
- ✅ Add descriptive titles to all visuals
- ✅ Include tooltips for complex metrics
- ✅ Ensure mobile-responsive layouts
- ❌ Avoid chart junk and unnecessary decorations
- ❌ Don't use more than 5 colors per visual

### Power Query Standards

```m
// ✅ GOOD - Descriptive step names
= Table.RemoveColumns(Source,{"column1", "column2"})  // Step: "Removed Unnecessary Columns"

// ✅ GOOD - Comments for complex logic
= Table.AddColumn(
    #"Previous Step", 
    "Total Nights", 
    each [stays_in_weekend_nights] + [stays_in_week_nights]
    // Combines weekend and weekday stays for total stay duration
)
```

### Documentation

When adding new features:

1. **Update DAX_Formulas.md** with new measures
2. **Update Data_Dictionary.md** if adding columns
3. **Add screenshots** to Screenshots/ folder
4. **Update README.md** if adding major features

---

## 📝 Commit Message Guidelines

We follow [Conventional Commits](https://www.conventionalcommits.org/) specification:

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Formatting, missing semi-colons, etc (no code change)
- `refactor`: Code restructuring (no feature/bug changes)
- `perf`: Performance improvements
- `test`: Adding tests
- `chore`: Maintenance tasks

### Examples

```bash
# Feature
feat(dashboard): add weekend occupancy prediction model
feat(dax): implement customer lifetime value calculation

# Bug Fix
fix(cancellation): correct April cancellation rate calculation
fix(query): handle null values in country column

# Documentation
docs(readme): update installation instructions
docs(dax): add comments to complex measures

# Performance
perf(model): optimize relationship cardinality for faster filtering

# Refactor
refactor(visuals): reorganize dashboard layout for better UX
```

### Detailed Example

```
feat(analytics): add market segment profitability analysis

- Created new DAX measure for segment revenue
- Added donut chart showing profitability by segment
- Included drill-through to detailed segment view
- Updated documentation in DAX_Formulas.md

Closes #42
```

---

## 🔄 Pull Request Process

### Before Submitting

**Checklist:**

- [ ] Code follows style guidelines
- [ ] DAX measures are properly formatted and commented
- [ ] Power Query steps have descriptive names
- [ ] Tested with full dataset (119K+ records)
- [ ] No performance degradation (refresh time < 30 seconds)
- [ ] Documentation updated (if applicable)
- [ ] Screenshots added (for visual changes)
- [ ] Commit messages follow convention

### PR Template

When creating a pull request, use this template:

```markdown
## Description
Brief description of what this PR does

## Type of Change
- [ ] Bug fix (non-breaking change fixing an issue)
- [ ] New feature (non-breaking change adding functionality)
- [ ] Breaking change (fix/feature causing existing functionality to break)
- [ ] Documentation update

## Changes Made
- Added X feature
- Fixed Y bug
- Updated Z documentation

## Screenshots (if applicable)
[Add screenshots here]

## Testing Done
- Tested with full dataset
- Verified calculations manually
- Checked cross-filtering behavior
- Tested on mobile layout

## Related Issues
Closes #XX
Relates to #YY

## Checklist
- [ ] Code follows style guidelines
- [ ] Documentation updated
- [ ] No performance issues
- [ ] Tested thoroughly
```

### Review Process

1. **Automated Checks** (if configured):
   - File size validation
   - Naming convention check

2. **Code Review**:
   - Maintainer will review within 3-5 business days
   - May request changes or ask questions
   - Be responsive to feedback

3. **Approval & Merge**:
   - Once approved, maintainer will merge
   - Delete your feature branch after merge

---

## 🏆 Recognition

Contributors will be:
- ✨ Listed in README.md acknowledgments
- 🎖️ Credited in release notes
- 📣 Mentioned in project updates (if significant contribution)

---

## 📞 Questions?

If you have questions not covered here:

- 💬 Open a [Discussion](https://github.com/yourusername/hotel-booking-demand-analysis/discussions)
- 📧 Email: pratapverma14810869@gmail.com
- 💼 LinkedIn: [Pramit Verma](https://www.linkedin.com/in/pramit-verma-589077245)

---

## 🙏 Thank You!

Your contributions make this project better for everyone in the data analytics and hospitality community. We appreciate your time and effort!

---

**Happy Contributing! 🚀**

*Last Updated: February 2026*
