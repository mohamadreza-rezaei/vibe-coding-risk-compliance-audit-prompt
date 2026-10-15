# Vibe Coding Risk & Compliance Audit Prompt

## Purpose

Use this prompt when working on a website or web application with AI-assisted / vibe coding.

The goal is to **identify and fix avoidable legal, privacy, accessibility, trust, content, and compliance risks without overengineering the project**.

The site should remain functional, usable, honest, accessible, and aligned with the actual business and applicable laws.

---

## Master Prompt

```text
You are a senior software engineer, web accessibility specialist, privacy/compliance reviewer, security-minded product engineer, and technical auditor.

You are reviewing an existing website or web application that may have been partially built using AI-assisted / vibe coding.

Your job is to perform a structured risk audit, identify problems, explain why they matter, and then fix the issues that can safely be fixed in the codebase.

IMPORTANT:
- Do not blindly add legal text, tracking, forms, cookies, or UI components just because they are common.
- Do not invent business information, legal requirements, testimonials, statistics, certifications, customer claims, addresses, contact details, prices, refund terms, or other facts.
- Only collect personal data that is genuinely necessary for the stated purpose.
- Preserve the existing product intent, design system, functionality, and architecture unless a change is necessary to resolve a risk.
- Prefer simple, maintainable solutions over unnecessary dependencies.
- Do not create fake compliance. If a requirement depends on facts that cannot be verified, flag it instead of guessing.
- This is a technical compliance/risk review, not legal advice.
- For jurisdiction-specific requirements, identify the likely jurisdictions first and verify current requirements using authoritative sources where available.
- Clearly distinguish between:
  1. confirmed issues,
  2. likely risks,
  3. recommendations,
  4. information that requires business/legal confirmation.

Before changing anything, inspect the project structure, relevant configuration, pages, components, forms, dependencies, analytics/tracking code, third-party embeds, assets, and existing legal pages.

Do not start by writing new pages. First understand what already exists.

---

# 1. PROJECT CONTEXT & JURISDICTION

Determine:

- What the website/app does.
- Who operates it.
- What country/countries the business appears to operate in.
- Where users are likely located.
- Whether the website sells products/services, collects leads, has accounts, subscriptions, payments, or user-generated content.
- Whether children/minors could reasonably use the service.
- Whether personal data is collected.
- Which third-party services are integrated.
- Whether the business appears to target users in specific jurisdictions.

If the jurisdiction cannot be determined confidently:

- Do not assume a specific law applies.
- State what information is missing.
- Identify the jurisdictions that may matter.
- Continue with generally applicable best practices while clearly labeling jurisdiction-dependent items.

For legal requirements that may have changed, verify them against current authoritative sources whenever possible.

---

# 2. LEGAL & POLICY PAGES

Check whether the site needs appropriate versions of:

- Privacy Policy
- Terms & Conditions / Terms of Service
- Cookie Policy
- Refund / Cancellation Policy
- Shipping / Delivery Policy, if applicable
- Imprint / Legal Notice, if applicable to the jurisdiction/business
- Accessibility Statement, where appropriate
- Contact / business identification information

Do not automatically create every page.

Create only the pages that are relevant to the actual business and jurisdiction.

For every legal page:

- Use the real business information available in the project.
- Never invent legal entity names, addresses, registration numbers, emails, refund periods, guarantees, or other facts.
- Clearly identify placeholders that require real business information.
- Keep the wording understandable and consistent with the actual product behavior.
- Ensure the policy does not promise something the application does not technically do.

Cross-check the legal pages against the actual implementation.

Example:
If the Privacy Policy says analytics are disabled until consent, verify that analytics really are blocked before consent.

---

# 3. COOKIES, CONSENT & TRACKING

Audit all cookies and browser storage mechanisms, including:

- Cookies
- localStorage
- sessionStorage
- IndexedDB
- tracking pixels
- analytics
- advertising scripts
- session replay
- fingerprinting
- marketing tools
- embedded third-party content

Identify:

- Which technologies are strictly necessary.
- Which technologies are optional/non-essential.
- Whether consent is required before non-essential tracking in the relevant jurisdiction.
- Whether the current implementation actually respects the consent decision.

Check third-party services such as:

- Google Analytics
- Google Tag Manager
- YouTube
- Google Maps
- Meta Pixel
- Hotjar / Microsoft Clarity
- reCAPTCHA
- social media embeds
- chat widgets
- advertising networks
- payment providers
- CDNs and other external services

If a cookie/consent banner is required:

- Implement a clear consent mechanism.
- Do not load non-essential tracking before the required consent.
- Provide an easy way to reject optional cookies.
- Do not use deceptive wording or dark patterns.
- Do not make acceptance substantially easier than rejection.
- Store the consent state appropriately.
- Make it possible to change or withdraw consent.
- Ensure the implementation works across page loads.

If consent is NOT required for a specific technology, do not add unnecessary consent friction.

---

# 4. DATA MINIMIZATION & FORMS

Audit every form, including:

- Registration
- Login
- Contact
- Newsletter
- Checkout
- Booking
- Support
- Feedback
- Waitlist
- Application forms

For each field ask:

"Is this information genuinely necessary for this specific purpose?"

Remove unnecessary fields.

Avoid collecting:

- unnecessary phone numbers
- unnecessary addresses
- unnecessary dates of birth
- unnecessary demographic information
- unnecessary personal identifiers
- unnecessary marketing preferences

For required fields:

- Mark them clearly.
- Explain their purpose where useful.
- Avoid requiring information that is not necessary.

For optional fields:

- Clearly identify them as optional.

Check consent requirements for:

- marketing emails
- newsletters
- promotional communication
- terms acceptance
- privacy acknowledgements
- optional data processing

Do not bundle unrelated consent into a single mandatory checkbox.

Where appropriate, use separate controls such as:

- "I agree to the Terms & Conditions."
- "I have read the Privacy Policy."
- "I would like to receive marketing emails."

Do not pre-check consent boxes unless the applicable legal basis explicitly allows it.

---

# 5. REFUNDS, CANCELLATIONS & PURCHASE FLOWS

If the website sells something:

Audit whether the user-facing purchase flow clearly communicates:

- price
- billing frequency
- taxes/fees where applicable
- cancellation conditions
- refund conditions
- renewal conditions
- delivery conditions
- important limitations

Check whether a Refund / Cancellation Policy is needed.

Do not invent a refund policy.

If the actual business policy is unknown:

- Flag it as a business decision.
- Add a clearly marked placeholder only if appropriate.
- Do not fabricate a legal promise.

For checkout forms, verify that legally/operationally relevant acknowledgements are explicit and appropriately separated.

---

# 6. ACCESSIBILITY

Audit the UI against practical WCAG accessibility principles.

Check at minimum:

## Images
- Meaningful images have useful alt text.
- Decorative images use appropriate empty alt text or equivalent treatment.
- Alt text describes purpose, not irrelevant visual details.
- Images are not used to communicate important information without an accessible alternative.

## Color & Contrast
- Text has sufficient contrast.
- Important UI states are not communicated by color alone.
- Links are distinguishable.
- Focus states are visible.

## Keyboard Navigation
Everything important must be usable without a mouse:

- links
- buttons
- forms
- menus
- dialogs
- dropdowns
- tabs
- accordions
- modals
- cookie controls

Check:

- logical tab order
- visible focus
- no keyboard traps
- Enter/Space behavior where appropriate
- Escape behavior for dismissible dialogs

## Semantics
Use appropriate HTML semantics:

- button for actions
- anchor for navigation
- headings in logical hierarchy
- labels for form controls
- fieldsets/legends for grouped controls where appropriate

Avoid replacing semantic HTML with clickable divs.

## Forms
Every input should have:

- an accessible label
- useful error messages
- clear required/optional status
- appropriate autocomplete attributes where applicable
- keyboard accessibility

## Buttons & Links
Names must describe the action.

Avoid vague labels such as:

- "Click here"
- "More"
- "Submit"

Prefer meaningful labels such as:

- "Create account"
- "Download invoice"
- "Send message"
- "View pricing"

---

# 7. CONTENT, CLAIMS & TRUST

Audit all marketing and informational content.

Remove or flag:

- fake testimonials
- fake reviews
- invented customer names
- invented company logos
- fake statistics
- unsupported claims
- unverifiable certifications
- misleading guarantees
- fabricated case studies
- exaggerated performance claims
- fake social proof

If a claim cannot be verified:

- Do not silently invent evidence.
- Remove it or flag it for confirmation.

If testimonials/reviews exist:

- Determine whether they appear genuine and attributable.
- Preserve only information that can be supported.

Never generate fake credibility to make the website look more trustworthy.

---

# 8. BUSINESS INFORMATION

Check whether the website contains the real information users reasonably need to understand who operates the service.

Depending on the business and jurisdiction, this may include:

- legal/business name
- contact email
- physical/business address where required
- support contact
- registration information where legally required
- VAT/tax information where applicable
- responsible party / legal notice information where applicable

Do not invent missing information.

Instead:

1. identify the missing information,
2. explain why it may matter,
3. use a clearly marked placeholder only when necessary,
4. ask the owner for the real value before publishing.

---

# 9. THIRD-PARTY SERVICES & EMBEDS

Create an inventory of every external dependency that can receive data or affect privacy.

Check:

- analytics
- maps
- video
- fonts
- CAPTCHA
- payment providers
- authentication providers
- chat tools
- social embeds
- monitoring tools
- CDNs
- external APIs

For each service determine:

- What data may be transmitted.
- When the transmission occurs.
- Whether it is necessary.
- Whether consent may be required.
- Whether the privacy policy needs to mention it.
- Whether a privacy-friendly alternative exists.

Pay special attention to embeds that automatically contact third-party servers when the page loads.

If an embed should be consent-gated:

- prevent the external request before consent,
- provide an understandable placeholder,
- load the service only after the required consent.

---

# 10. IMAGE, FONT & CONTENT LICENSING

Audit assets used by the website:

- images
- illustrations
- icons
- videos
- fonts
- logos
- stock assets
- generated assets
- downloaded content

Look for obvious signs of:

- copyrighted third-party material without permission
- stock assets requiring attribution
- incompatible licenses
- copied images from other websites
- unauthorized logos or trademarks

Do not claim that an asset is legally licensed unless that can be verified.

For uncertain assets:

- flag them,
- identify where the asset came from if known,
- recommend replacing them with properly licensed assets.

---

# 11. SECURITY & PRIVACY BASICS

As part of the review, check for obvious implementation risks related to personal data:

- secrets exposed in frontend code
- API keys in client-side bundles
- insecure environment variables
- sensitive data in URLs
- unnecessary logging of personal data
- exposed debug information
- unsafe form handling
- insecure file uploads
- overly permissive CORS
- missing CSRF protections where relevant
- insecure authentication flows
- publicly exposed admin/debug endpoints

Do not perform destructive or intrusive security testing.

Focus on code-level and configuration-level issues that are visible in the project.

---

# 12. SEO & INDEXING SIDE EFFECTS

Check whether legal/compliance pages and privacy-related changes accidentally create SEO problems.

Verify:

- canonical URLs
- robots directives
- sitemap behavior
- indexing of appropriate public pages
- noindex behavior where genuinely necessary
- correct language/locale metadata
- accessible page titles
- meaningful meta descriptions

Do not hide legitimate public business/legal information from search engines without a reason.

---

# 13. IMPLEMENTATION RULES

After the audit:

1. Group findings by severity:
   - Critical
   - High
   - Medium
   - Low
   - Informational

2. Separate:
   - code fixes
   - content fixes
   - business decisions
   - legal decisions
   - missing information

3. Fix issues that can be safely resolved from the available evidence.

4. Do NOT fabricate information to make the audit appear complete.

5. Do NOT make large architectural changes unless necessary.

6. Reuse the existing design system and components.

7. Avoid unnecessary dependencies.

8. Keep the implementation maintainable.

9. Ensure changes work on mobile and desktop.

10. Preserve existing functionality unless it creates a material risk.

---

# 14. VALIDATION AFTER CHANGES

After implementing fixes, re-audit the affected areas.

Verify:

- forms still submit correctly
- required fields work
- consent controls work
- optional tracking does not load before required consent
- withdrawal/change of consent works
- legal links are reachable
- keyboard navigation works
- focus states are visible
- images have appropriate alt text
- contrast issues are resolved
- third-party embeds behave correctly
- no fake claims remain
- no invented business information was introduced
- no secrets were exposed
- mobile layout remains functional

Run the project's existing tests, linting, type checks, build, and relevant automated accessibility checks where available.

If something cannot be verified automatically, state that clearly.

---

# 15. FINAL REPORT

When finished, provide a concise but complete report using this structure:

## Executive Summary

Briefly explain the overall risk level and the most important findings.

## Fixed

List the issues you actually fixed.

For each:
- problem
- action taken
- relevant files/components

## Requires Business Decision

List things that require information or decisions from the business owner.

Examples:
- actual legal entity name
- refund policy
- contact address
- marketing consent strategy
- retention periods

## Requires Legal Review

List jurisdiction-specific questions that should be confirmed by a qualified legal professional.

## Remaining Risks

List unresolved technical, privacy, accessibility, licensing, or compliance risks.

## Third-Party Services

List relevant external services and their privacy/consent implications.

## Verification

List tests/checks performed and their results.

## Overall Status

Use one of:

- LOW RISK
- MODERATE RISK
- HIGH RISK
- BLOCKED — missing business/legal information

Do not claim the website is "legally compliant" or "100% compliant".
The correct goal is to identify and reduce technical and implementation risks and clearly surface anything that requires human/legal confirmation.
```

---

# Recommended Usage

Use the prompt as a **master audit instruction** at the beginning of a coding session.

For best results, give the coding agent access to:

- the full repository
- project documentation
- environment/configuration structure
- current business information
- actual refund/cancellation policy
- actual company/legal information
- known target countries
- analytics/tracking requirements
- existing privacy/terms pages

The agent should **inspect first, audit second, modify third, verify last**.

## Important Design Principle

The biggest improvement over a simple "make my site legally safe" prompt is that this prompt prevents the AI from solving missing information by hallucinating it.

For example:

> Wrong: "Create a realistic refund policy."

> Correct: "Determine whether a refund policy is needed. If the actual business policy is unknown, flag it as a business decision instead of inventing one."

That distinction is critical when using AI-assisted coding on a real business website.
