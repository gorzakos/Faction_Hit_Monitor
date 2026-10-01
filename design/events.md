# Relevant events
An event is a grouping of related log lines. For example, a goblin dies, you gain experience, you level up, your faction with goblins goes down, and your faction with Cabilis guards go up. Relevant events are events that can help us forensically estimate how much faction is adjusted. If discreet events can have their faction adjustments calculated, then estimating total earned faction is just adding all those faction adjustments together.

## Zone transitions
 - Zones describe available faction adjustments.
 - Transitions discard all potential triggers seen so far.

## Faction Events
 - Tight time duration, same or next second
 - Multiple factions possible
 - Unique factions, seeing the same faction would indicate a 2nd event
 - Only faction types listed, values must be inferred from trigger.

## Potential Triggers

### Quest Message
 - Evaluated by timestamp for connection to faction adjustment events
   - Primary, would be same or next second.
  - Not all quest messages have faction events, nor all quests quest messages
  - All faction events with quest message are considered High Confidence
  - Can be discarded after association with faction event


### Death Message
 - Evaluated by timestamp for connection to faction adjustment events
   - Primary, would be same or next second.
  - Not all death messages have faction events
  - All faction events with death message are considered High Confidence
  - Can be discarded after association with faction event
   
### Combat Engagement
 - Evaluated by timestamp for connection to faction adjustment events
   - Secondary and error prone, prefer death/quest messages.
   - Faction events tied to combat engagement are considered Low Confidence
 - Three potential options
   - melee combat, with any source and target
   - threat spells, either to or from player
   - aggro message
 - Can imperfectly discard after an arbitrary duration threshold
   - Not likely to get faction hits from a mob not seen in the last 3 minutes
   - Cannot be discarded after faction adjustments, due to duplicate mob names
   - When multiple comparable events occur, only the newest one is relevant

### Null
 - Evaluated only by comparing faction event with zone possibilities
   - Could be quest with no message (like Rebby's whiskers)
   - Could be aggro from a mob with no combat triggers 
 - Faction events associated with Null have lowest confidence.
