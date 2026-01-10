# Guidance for AI Agents Working on This Repository

This document provides guidelines for AI agents (including GitHub Copilot) making updates to this documentation repository about the UK implementation of the Akoma Ntoso (AKN) XML standard for legislation.

## About This Repository

This is a **documentation-only repository** that describes how the Akoma Ntoso XML standard for legislation is being applied to UK legislation. It documents the Lawmaker data model, which uses XML compliant with the AKN schema with some extensions and restrictions.

## Key Guidelines

### 1. Link to Official Akoma Ntoso Documentation

When mentioning any AKN elements, attributes, or concepts in the documentation, **always include links to the relevant official Akoma Ntoso documentation**.

**Primary documentation sources:**

- **Part 2 (Specifications)**: https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html
  - Use this for specific element definitions and technical specifications
  - Link to specific element anchors when discussing particular elements (e.g., `#element_hcontainer` for the hcontainer element)

- **Part 1 (Vocabulary)**: https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html
  - Use this for conceptual information about AKN vocabulary and structure
  - Reference when discussing overall AKN concepts, patterns, or design principles

**Note:** Ensure you are linking to the **v1.0/os** (OASIS Standard) version, not older versions like csd02 or csd03.

### 2. Ensure Compliance with the Akoma Ntoso Schema

All content in this documentation must be compliant with and not contradict the official Akoma Ntoso schema.

**Official schema location:**
- https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/schemas/akomantoso30.xsd

**Before making changes:**
- Verify that any elements, attributes, or structural patterns mentioned exist in the schema
- Check that described element hierarchies and nesting rules are valid according to the schema
- Ensure attribute values conform to schema-defined enumerations or patterns
- Do not suggest or document uses that would violate schema constraints

**When documenting extensions:**
- Clearly distinguish between standard AKN elements and UK-specific extensions (typically in the `ukl:` namespace)
- Document why extensions are necessary and how they relate to the standard

### 3. Check Against Example Files

Before committing changes to the documentation:

**If example files exist** (e.g., in an `examples/` folder):
- Review relevant example files to ensure documentation accurately reflects actual usage
- Verify that any patterns or structures described in the documentation match the examples
- Raise any inconsistencies between documentation and examples for review
- When adding new documentation, check if there are examples that illustrate the concept

**Handling inconsistencies:**
- If you find discrepancies between documentation and examples, do not automatically change either
- Note the inconsistency and ask for clarification about which is correct
- Examples may represent actual implementation while documentation represents intent
- Both may need updating to achieve consistency

### 4. Maintain Neutral, Factual Tone

This documentation should be objective and focused on describing the UK AKN implementation:

**Avoid:**
- Overly-opinionated statements about the AKN standard
- Criticisms of the AKN schema design or structure
- Subjective judgments about whether AKN elements are "good" or "bad"
- Speculative statements about why AKN was designed in a particular way

**Instead:**
- Use neutral, descriptive language
- Focus on documenting how UK legislation uses AKN elements
- When documenting workarounds or non-standard uses, explain the practical need
- Describe decisions and rationales without being judgmental

**Examples:**

❌ "AKN's lack of a @name attribute on blockContainer is a poor design choice"

✅ "The AKN standard does not provide a @name attribute for //blockContainer elements. To address the need for consistent naming, this implementation uses the @class attribute to hold the name."

❌ "The confusing distinction between tblock and blockContainer"

✅ "The AKN standard provides //tblock and //blockContainer elements with similar capabilities but limited guidance on when to use each."

### 5. Include XML Example Snippets

To make the documentation clear and practical, include XML code examples where helpful:

**Guidelines for XML examples:**
- Ensure all examples are **valid according to the AKN schema**
- Use proper XML formatting with appropriate indentation
- Include relevant attributes that would typically be present
- Use realistic content that illustrates the element's purpose
- Keep examples concise but complete enough to be meaningful
- Use markdown code blocks with `xml` language identifier for syntax highlighting

**Example format:**
```xml
<hcontainer name="step" eId="sec_1_step_1">
  <num>Step 1</num>
  <content>
    <p>Determine the relevant date for the transaction.</p>
  </content>
</hcontainer>
```

**When to include examples:**
- When introducing a new element or pattern
- When describing complex structural relationships
- When explaining UK-specific extensions or variations from standard AKN
- When clarifying potentially ambiguous concepts

**When examples might not be needed:**
- For very simple elements that are self-explanatory
- When the text already references external comprehensive examples
- For metadata or attributes that are better shown in context of a larger example elsewhere

### 6. Maintain Consistency with Existing Documentation

When updating or adding content:
- Follow the existing structure and organization patterns
- Use terminology consistent with other parts of the documentation
- Match the existing writing style and level of detail
- Preserve existing links and cross-references unless they need updating
- Ensure examples follow similar patterns to existing examples in the repository

### 7. Document Structure and Organization

This repository includes:
- **Root level documents**: High-level concepts and principles
- **data-dictionary/**: Detailed element-by-element documentation
- Each document should be focused on a specific aspect of the model
- Maintain clear navigation between related documents

### 8. Quality Checklist Before Committing

Before finalizing changes, verify:

- [ ] All mentioned AKN elements have links to official documentation (v1.0/os)
- [ ] Content is compliant with the AKN schema (checked against XSD if needed)
- [ ] Consistency with example files has been verified (if examples exist)
- [ ] Language is neutral and factual, without undue criticism
- [ ] XML examples are included where helpful and are schema-compliant
- [ ] Changes maintain consistency with existing documentation style
- [ ] Cross-references and links are accurate and working
- [ ] Markdown formatting is correct and renders properly

## Additional Notes

### Understanding the Context

The Lawmaker system uses AKN with some necessary extensions for UK legislative needs. The documentation:
- Explains both standard AKN usage and UK-specific patterns
- Reflects practical implementation decisions made for real UK legislation
- Balances adherence to AKN standards with pragmatic solutions

### When in Doubt

If uncertain about:
- Whether something complies with AKN schema → Check the XSD
- Whether a description matches examples → Review example files
- Whether tone is appropriate → Err on the side of neutral, factual description
- Whether to include an example → More examples are generally better for clarity

## Resources

- **Akoma Ntoso Official Site**: http://www.akomantoso.org/
- **OASIS LegalDocML TC**: https://www.oasis-open.org/committees/legaldocml/
- **AKN Core 1.0 Specifications (Part 2)**: https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/akn-core-v1.0-os-part2-specs.html
- **AKN Core 1.0 Vocabulary (Part 1)**: https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part1-vocabulary/akn-core-v1.0-os-part1-vocabulary.html
- **AKN Core 1.0 Schema (XSD)**: https://docs.oasis-open.org/legaldocml/akn-core/v1.0/os/part2-specs/schemas/akomantoso30.xsd
