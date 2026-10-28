KH1FM Kingdom Key Offhand Integrated v6 Visual Contact (V272)

This test build adds the confirmed textured visual duplicate to the integrated
controller and fixes its contact gate. Your previously working trail scheduler
and all native hook bytes are unchanged from v5.

Damage still requires BOTH fresh offhand blade proximity and a matching native
primary attack-builder event against the selected enemy. A hit made only by
the offhand blade while the main weapon misses is NOT implemented by this build.
That remaining collision path needs further native investigation. This build
must not be treated as the completed independent offhand damage implementation.

INSTALL
1. Fully close KH1FM.
2. Extract the ZIP. Install this folder as one OpenKH mod and enable it.
   Use the folder containing mod.yml. Leave the three MDLS source files at
   that folder's root; the manifest already targets the game's obj/ paths.
3. Disable older dual-wield asset experiments. Make this mod's normal-Sora and
   Kingdom Key assets the effective versions if another model mod conflicts.
4. Move older integrated offhand Lua versions out of the active scripts folder.
   Keep old offhand damage, marker, visual, trail and contact tests disabled.
5. Copy lua/KH1FM_KingdomKey_Offhand_Integrated_v6_VisualContact.lua into the
   active scripts folder you have been using. The asset mod alone does not
   activate LuaBackend scripts; this copy is required.
6. Apply/build the enabled OpenKH mod and launch a fresh game process.
   Do not install or reload this build with F1.
7. Use normal Sora, equip Kingdom Key and stand idle until TRAIL READY.
   After a scene/actor reload, allow the idle baseline to finish again.

VISUAL DUPLICATE
The eleven MDLS/CVBL/DDS assets are byte-for-byte copies of the confirmed
KH1FM_KingdomKey_DualWield_Confirmed50_v25 visual baseline: native descriptor 6,
palette slot 9 bound to joint 205, the confirmed 50-degree tilt, and its matching
textures. No appended descriptor, joint-206 experiment, WPN container replacement
or moveset edit is included. The model's blade length matches the existing
trail/contact segment.

Once the current model route is verified, Lua shows this duplicate for Kingdom
Key and hides it for other weapons using only its four-byte packet marker.
The original asset loads with its original visible marker; the weapon gate
takes over after the guarded model-loading interval. Halloween Town, Atlantica
and alternate character/form models are not covered.

CONTACT DAMAGE AND EFFECTS
The request closes on every sample and opens only when the current blade
segment is within the existing 56-world-unit bound of validated enemy pose
points during the native basic-attack window. This is a proximity approximation,
not mesh-to-mesh collision. Prediction and the old contact latch are disabled.
Leaving contact, losing the pose, changing targets or ending the attack closes
the request. A completed native result remains available for qualification.

The existing selector-4 native transaction and native/verified Equipment-LIMIT
formula remain in use; there are no direct HP writes. A selected, validated
enemy is required. Training dummies, missing-model entities and refused target
classes remain excluded. Refusal messages do not indicate that trails stopped.
The controller checks that the duplicate belongs to the current Sora model and
is visible before publishing shared contact geometry for damage and hit effects.

IN-GAME CHECK
First confirm the visible duplicate and the attacks/trails that already worked.
Then lock onto a real supported enemy, allow target setup to finish, and try
ground/aerial basic combos. Check the extra damage and enemy HP response; an
impact effect or sound alone does not prove that damage was applied.

Useful log evidence includes:
  MARKER GATE READY
  DAMAGE POSE READY
  OFFHAND CONTACT OBSERVED / REQUEST ARMED
  EQUIPMENT-INTEGRATED OFFHAND RESULT ... qualified=true
  TARGET HP LOSS

ARMED REQUEST WITHOUT NATIVE ATTEMPT identifies a proximity sample for which
no matching native builder event followed. It is not a successful offhand hit.
VISUAL ASSET REQUIRED means the active Sora model does not contain the expected
duplicate; check that the OpenKH assets were actually applied.

Return the full log after the test:
  KH1FM_KingdomKey_Offhand_Integrated_v6_VisualContact_Log.txt
It is written beside the active Lua. Include console output if the mod stops.

VALIDATION
87 simulated Lua 5.4 scenarios passed: 24 startup/route/cleanup, 18 transition,
22 initialized-asset re-entry, and 23 visual/contact cases. The new cases use
the actual packaged CVBL with simulated native relocation and run the real
marker validator, damage initializer, target-pose contact sampler and shared
pose publisher. They reproduce v5's contact latch and test its removal,
weapon swaps, missing geometry, actor/model reloads and stale packet rejection.
Existing re-entry texture fixtures are synthetic checksum-matching data.

All eleven asset files match the confirmed source hashes, and all manifest
sources resolve. The embedded trail scheduler, native image and native symbol
table match v5 exactly. These checks do not substitute for the fresh-process
KH1FM test of this integration or establish independent offhand-only damage.
