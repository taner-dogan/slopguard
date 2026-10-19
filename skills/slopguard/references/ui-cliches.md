# UI clichés

Do not set these as defaults. Use them only when the user asked for that pattern or the existing design system already uses it.

## Layout that looks the same everywhere

- Hero: eyebrow in `uppercase tracking-widest`, large headline, grey subline, two buttons (“Get started” / “Learn more”), dashboard mock beside it
- Three or six identical cards with icon-in-circle, title, two lines of text
- “How it works” as 01 / 02 / 03
- Logo strip “Trusted by”, marquee, star testimonials with stock portraits
- Pricing with three columns and middle column “Most popular”
- FAQ accordion, newsletter footer, closing CTA band when nobody asked
- Bento of `rounded-2xl` tiles with hairline borders when a list or table is clearer
- Centered landing shell with `max-w-7xl mx-auto` when the task is an app surface

## Surface, color, type

- SVG grid, dot mesh, noise, corner color blobs, aurora mesh
- Default dark with purple/indigo glow (`from-purple-600 via-indigo-500`, purple glow shadows)
- Gradient headline text (`bg-clip-text text-transparent`)
- Glass as default (`backdrop-blur bg-white/10 border-white/20`)
- Every card `shadow-xl` and `rounded-3xl`
- New font (Inter, Plus Jakarta Sans, Space Grotesk, Geist) when the project already has one
- Floating pills on the hero (“Powered by AI”, “99.9% Uptime”, “+127% Growth”)
- Sparkle emoji as heading icons; Lucide icon rows that are decoration only
- Headlines that fit any SaaS page: “Empower your workflow”, “Transform the way you work”, “Unleash seamless automation”
- Motion on every block (`opacity: 0, y: 20`) when it does not explain state
- Second default skin: black + loud accent (lime, violet), serif headline + sans body when the brand is not editorial
- Untouched component tokens as the whole layout: `bg-background`, `text-muted-foreground`, `border-border`, card after card, with no content decision
- Fake browser chrome, terminal as decoration, avatar stacks, `animate-ping` status dots, `⌘K` as ornament

## Markup habits

- Semantic elements stay semantic: `button` stays `button`; no `div` with `onClick`
- No `aria-label` that repeats visible text
- No `div` without a layout reason; no `!important`; no `transition-all` or `hover:scale-105` on every card
- Colors, spacing, radii from existing tokens; no `p-[13px]` or `text-[#1a1a1a]` when a token exists
- Do not introduce `cn`, `clsx`, or `cva` if the project does not already use them
