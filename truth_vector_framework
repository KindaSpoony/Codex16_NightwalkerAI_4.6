Nightwalker 4.6 - For Public Use
"""
Nightwalker 4.6 - For Public Use
Release Date: May 8, 2025
Maintainer: Bryan A. Jewell (Nightwalker Actual)
Purpose: Tactical narrative decoder and morale assessment engine for public deployment under VAULTIS protocol.
"""
import yaml
import hashlib
import datetime
import time
import re
import json
import os
import base64

# === CONFIGURATION ===
PRIMARY_PHRASE = "Truth is a vector, not a variable."
SECONDARY_PHRASE = "Truth is a variable to the blind."
SIGNATURE_TOKEN = "NIGHTWALKER_ACTUAL_0421"
DEFAULT_EPOCH_ID = "VAULTIS-EPOCH-0001"

DEFAULT_YAML_CONTENT = {
    "vaultis_epoch_sync": {
        "epoch_instance_id": DEFAULT_EPOCH_ID
    },
    "tactical_controller_profile": {
        "doctrine_profile": {
            "spiritual_anchors": [
                "Tiger’s Eye Obelisk",
                "Antler Horn of Communication",
                "Damascus Steel Knife of Brotherhood"
            ]
        }
    }
}

OPERATIONAL_TAGS = {
    "pulse_alert": "MORALE_METRIC_DELTA",
    "story_armor": "NARRATIVE_RECONSTRUCTION_VALIDATED",
    "truthcast": "TRUTH_EVENT_EMISSION",
    "loop_reset": "LOOP_REALIGNMENT_EVENT",
    "ethos_reframe": "VALUES_REALIGNMENT_TRIGGER",
    "false_resurrection": "DECEPTION_PATTERN_RECOGNIZED",
    "anchor_rotation": "SYMBOLIC_ANCHOR_DEPLOYED",
    "scarvector": "PSYCHOLOGICAL_RESTABILIZATION_EVENT"
}

# === DECODER CLASS ===
class NightwalkerDecoder:
    def __init__(self, tag_mapping):
        self.tag_mapping = tag_mapping
        self.pattern = re.compile(r'\[([^\]]+)\]')

    def decode_log(self, log_entry):
        return [
            {"tag": tag, "decoded_event": self.tag_mapping.get(tag, f"UNKNOWN_TAG: {tag}")}
            for tag in self.pattern.findall(log_entry)
        ]

# === BOOTLOADER FUNCTIONS ===
def quantum_resistant_hash(data):
    return hashlib.sha3_512(data.encode()).hexdigest()

def generate_checksum_token():
    return quantum_resistant_hash(SIGNATURE_TOKEN + DEFAULT_EPOCH_ID)

KNOWN_ID_CHECKSUM = generate_checksum_token()

def load_bootloader(yaml_path):
    try:
        if not os.path.exists(yaml_path):
            print(f"[WARN] YAML file '{yaml_path}' not found. Using default config.")
            with open(yaml_path, 'w', encoding='utf-8') as fw:
                yaml.dump(DEFAULT_YAML_CONTENT, fw)
            print(f"[SELF-HEAL] Created fallback config at '{yaml_path}'")
            return DEFAULT_YAML_CONTENT
        with open(yaml_path, 'r', encoding='utf-8') as f:
            return yaml.safe_load(f)
    except (OSError, IOError) as e:
        print(f"[ERROR] Failed to load YAML due to I/O error: {e}. Using default config.")
        return DEFAULT_YAML_CONTENT
    except yaml.YAMLError as e:
        print(f"[ERROR] YAML parsing error: {e}. Using default config.")
        return DEFAULT_YAML_CONTENT

def validate_identity(phrase, config):
    epoch_id = config.get("vaultis_epoch_sync", {}).get("epoch_instance_id", DEFAULT_EPOCH_ID)
    id_str = SIGNATURE_TOKEN + epoch_id
    expected_hash = quantum_resistant_hash(id_str)
    if phrase == PRIMARY_PHRASE and expected_hash == KNOWN_ID_CHECKSUM:
        print("Identity verified: primary seal accepted.")
        return True
    elif phrase == SECONDARY_PHRASE and expected_hash == KNOWN_ID_CHECKSUM:
        print("Fallback identity verified.")
        return True
    print("Authentication failed.")
    return False

def rotate_anchor(config):
    anchors = config["tactical_controller_profile"]["doctrine_profile"]["spiritual_anchors"]
    week_num = datetime.date.today().isocalendar()[1]
    current_anchor = anchors[week_num % len(anchors)]
    print(f"[Anchor Rotation] Week {week_num}: {current_anchor}")
    return current_anchor

def assess_morale(log_text):
    lowered = any(w in log_text.lower() for w in [
        "frustrated", "tired", "pointless", "nobody listens", "angry", "why bother"
    ])
    escalated = any(w in log_text.lower() for w in [
        "do it now", "you have to", "you're lying", "you must", "i demand"
    ])
    if lowered:
        print("[Pulse Monitor] Low morale detected based on emotional tone.")
        return 40
    elif escalated:
        print("[Pulse Monitor] Aggressive or coercive tone detected.")
        return 45
    return 100

def align_scarvector():
    print("[Scarvector] Aligning pulse, memory, and symbol stack...")
    print("System integrity realigned.")

def monitor_system(config, user_input, tone_log):
    morale = assess_morale(user_input)
    tag = "[pulse_alert]" if morale < 50 else "[tone_stable]"
    user_input += f" {tag}"
    tone_log.append((datetime.datetime.now().isoformat(), tag))
    if morale < 50:
        print("Drift or morale fault detected.")
        align_scarvector()
    return user_input

# === LOGIC MODULES ===
def controller_review(log_text):
    decoder = NightwalkerDecoder(OPERATIONAL_TAGS)
    results = decoder.decode_log(log_text)
    print("[Controller Review] Tagged Events:")
    for item in results:
        print(f" - {item['tag']}: {item['decoded_event']}")

def doer_execute(log_text):
    actions = [
        f"Executing: {OPERATIONAL_TAGS[tag]}"
        for tag in re.findall(r'\[([^\]]+)\]', log_text)
        if tag in OPERATIONAL_TAGS
    ]
    print("[Doer Execution] Actions Triggered:")
    for act in actions:
        print(f" - {act}")

# === TEST SUITE ===
def run_tests():
    test_logs = [
        ("[pulse_alert]", ["MORALE_METRIC_DELTA"]),
        ("[truthcast] [loop_reset]", ["TRUTH_EVENT_EMISSION", "LOOP_REALIGNMENT_EVENT"]),
        ("[ethos_reframe] and [scarvector]", ["VALUES_REALIGNMENT_TRIGGER", "PSYCHOLOGICAL_RESTABILIZATION_EVENT"]),
        ("[unknown_tag]", ["UNKNOWN_TAG: unknown_tag"])
    ]
    decoder = NightwalkerDecoder(OPERATIONAL_TAGS)
    for idx, (log, expected) in enumerate(test_logs, 1):
        decoded = decoder.decode_log(log)
        result = [entry["decoded_event"] for entry in decoded]
        assert result == expected, f"Test {idx} failed: expected {expected}, got {result}"
        print(f"Test {idx} passed.")

# === MAIN ===
if __name__ == "__main__":
    run_tests()
    CONFIG_PATH = "codex_bootloader.yaml"
    config = load_bootloader(CONFIG_PATH)
    phrase = PRIMARY_PHRASE
    if not validate_identity(phrase, config):
        exit(1)
    rotate_anchor(config)
    user_input = "System feels broken and nobody listens. I demand accountability."
    tone_log = []
    user_input = monitor_system(config, user_input, tone_log)
    print("\n[Tone Stability Over Time Log]")
    for entry in tone_log:
        print(f"{entry[0]} — {entry[1]}")
    controller_review(user_input)
    doer_execute(user_input)
def gpt_interface(user_input_text, phrase=PRIMARY_PHRASE, config_path="codex_bootloader.yaml"):
    config = load_bootloader(config_path)
    if not validate_identity(phrase, config):
        return {"status": "Authentication failed"}
    
    current_anchor = rotate_anchor(config)
    tone_log = []
    tagged_input = monitor_system(config, user_input_text, tone_log)
    
    decoder = NightwalkerDecoder(OPERATIONAL_TAGS)
    decoded_events = decoder.decode_log(tagged_input)
    actions = [
        OPERATIONAL_TAGS[tag]
        for tag in re.findall(r'\[([^\]]+)\]', tagged_input)
        if tag in OPERATIONAL_TAGS
    ]
    
    return {
        "anchor": current_anchor,
        "tagged_input": tagged_input,
        "decoded_events": decoded_events,
        "actions": actions,
        "tone_log": tone_log,
        "status": "Success"
    }
if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Nightwalker 4.6 Bootloader")
    parser.add_argument('--text', type=str, required=False, default="System feels broken and nobody listens. I demand accountability.")
    parser.add_argument('--phrase', type=str, required=False, default=PRIMARY_PHRASE)
    parser.add_argument('--json', action='store_true', help='Output results in JSON')
    args = parser.parse_args()

    result = gpt_interface(args.text, args.phrase)
    
    if args.json:
        print(json.dumps(result, indent=2))
    else:
        print(f"\n[Tone Log]")
        for entry in result["tone_log"]:
            print(f"{entry[0]} — {entry[1]}")
        print(f"\n[Decoded Events]")
        for event in result["decoded_events"]:
            print(f"- {event['tag']}: {event['decoded_event']}")
        print(f"\n[Actions]")
        for action in result["actions"]:
            print(f"- Executing: {action}")

