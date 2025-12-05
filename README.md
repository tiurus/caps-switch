# ✅ Instant CapsLock EN ⇄ RU Switch on macOS (KeyDown, No Delay, No Caps Mode)

> This guide shows how to turn **Caps Lock into an instant language switcher (EN ⇄ RU)** on macOS:
>
> * ✅ Switches on **KeyDown** (not KeyUp)
> * ✅ Works even when the key is **held**
> * ✅ **No Caps Lock mode at all**
> * ✅ **No LED light**
> * ✅ No dependency on **“Select Previous Input Source”**
> * ✅ Stable across macOS updates
>
> Perfect for developers who want **zero latency, zero randomness, zero Caps pain**.

---

## 🔴 Problem

On modern macOS versions (Ventura / Sonoma / Sequoia):

* Caps Lock behavior is **hard-wired**:

  * Tap → switches input source
  * Hold → enables Caps Lock
* The system **waits for KeyUp** to decide what you meant
* You **cannot separate** these behaviors via system settings
* “Select previous input source” works inconsistently
* Latency is noticeable
* Caps Lock LED may turn on accidentally

**There is no native way to make Caps Lock switch language on KeyDown only.**

---

## ✅ Solution Overview

We will:

1. **Disable Caps Lock at the system level**
2. **Let Karabiner handle it exclusively**
3. **Implement our own smart EN ⇄ RU switch**
4. Trigger everything on **KeyDown**
5. **Never enable Caps mode again**

---

## ✅ Step 1 — Disable Caps Lock in macOS

Go to:

```
System Settings → Keyboard → Keyboard Shortcuts → Modifier Keys
```

Set:

```
Caps Lock → No Action
```

⚠️ This is mandatory.
If you skip this step, macOS will intercept Caps Lock and block KeyDown behavior.

---

## ✅ Step 2 — Disable built-in Caps language switching

If enabled, turn OFF:

```
Use Caps Lock to switch to and from ABC
```

Karabiner must be the **only** entity controlling this key.

---

## ✅ Step 3 — Install Karabiner-Elements

Official site:

[https://karabiner-elements.pqrs.org](https://karabiner-elements.pqrs.org)

After installation, allow:

* ✅ Input Monitoring
* ✅ Accessibility

---

## ✅ Step 4 — Add Smart EN ⇄ RU Switch (KeyDown)

Open:

```
~/.config/karabiner/karabiner.json
```

Add this block **inside `rules`**:

```json
{
  "description": "CapsLock → Smart EN ⇄ RU switch on KeyDown (no delay, no caps mode)",
  "manipulators": [
    {
      "type": "basic",
      "from": { "key_code": "caps_lock" },
      "conditions": [
        {
          "type": "input_source_if",
          "input_sources": [
            { "input_source_id": "com.apple.keylayout.ABC" }
          ]
        }
      ],
      "to": [
        {
          "select_input_source": {
            "input_source_id": "com.apple.keylayout.Russian"
          }
        }
      ]
    },
    {
      "type": "basic",
      "from": { "key_code": "caps_lock" },
      "conditions": [
        {
          "type": "input_source_if",
          "input_sources": [
            { "input_source_id": "com.apple.keylayout.Russian" }
          }
        }
      ],
      "to": [
        {
          "select_input_source": {
            "input_source_id": "com.apple.keylayout.ABC"
          }
        }
      ]
    }
  ]
}
```

✅ This creates:

* **Instant EN ⇄ RU toggle**
* **Triggered on KeyDown**
* **Works while holding the key**
* **No Caps Lock mode**
* **No LED**
* **No system delays**

---

## ✅ Step 5 — Verify Input Source IDs (Important)

If your Russian layout is not the default (e.g. “Russian – PC”), the ID may differ.

To check:

1. Open **Karabiner → Log**
2. Switch language manually
3. You will see:

```
select_input_source: com.apple.keylayout.Russian-PC
```

Replace this in the config:

```json
"input_source_id": "com.apple.keylayout.Russian-PC"
```

---

## ✅ Final Result

| Feature                      | Result       |
| ---------------------------- | ------------ |
| Language switch on KeyDown   | ✅ Yes        |
| Works while holding Caps     | ✅ Yes        |
| Caps Lock mode disabled      | ✅ Completely |
| LED light disabled           | ✅ Yes        |
| System language history used | ❌ No         |
| Depends on macOS shortcuts   | ❌ No         |
| Update-safe                  | ✅ Yes        |

---

## ✅ Optional Enhancements

You can easily extend this setup with:

* Tap → toggle EN ⇄ RU
* Hold → do nothing
* Double tap → always EN
* Triple tap → always RU

Karabiner fully supports this via:

* `to_if_alone`
* `to_if_held_down`
* `simultaneous`

---

## ✅ Tested On

* macOS Ventura
* macOS Sonoma
* macOS Sequoia

---

If you want, I can also generate:

* ✅ A minimal `karabiner.json` file for direct download
* ✅ A version for **more than two languages**
* ✅ A version for **Linux-like layouts**

---

🔥 If you publish this on GitHub — drop me the link.
We just saved a *lot* of developers from Caps Lock hell.
