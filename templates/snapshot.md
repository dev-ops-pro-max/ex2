# Channel Balance Snapshots

Fill in one table per exercise as you go. Amounts in satoshis (msat / 1000).
`local`/`remote` are from the perspective of the node listed.

## Table 1 — Exercise 1 (invoice)

| Item | Value |
|------|-------|
| Node alias / id | YELLOWWATER / 0317dbb0ff1c431a8567f8bbbccc50f7a2cd8aa0ec82861e555ea82001fca21a20 |
| On-chain funds (listfunds, sat) | 101 blocks mined to Alice |
| Invoice label | coffee-payment |
| Amount (sat) | 50000 |
| Description | Coffee Payment |
| Expiry (s) | 3600 |
| BOLT11 | lnbcrt500u1p4d3pkvsp55x944c0yasfewh7xyuapk4hp05l2zncqk8cyeyj8xjhq6ryceg9spp5pq5xfttc5jsugncgdaguu9m37lsga7ym548tyq5rl9tuzarzvptqdqhgdhkven9v5s9qcted4jkuaqcqp29qxpqysgqxmqxs56x3vwhe2yfnact48um6f5d8aag24s3uy4vksr3dak86l2nsggl7x7fgqr64aqwec0ptkv9h67nj8a46c5e9ll2vkmwc5espsgp73pl2m |
| decodeinvoice verified? | N/A (command not available in v24.05) |
| listinvoices shows status=unpaid, payee=self? | [x] |

## Table 2 — Exercise 2 (Alice → Bob channel)

| Node | Channel id | Capacity (sat) | Local bal (sat) | Remote bal (sat) | State |
|------|------------|----------------|-----------------|------------------|-------|
| Alice | 102x1x0 | 500000 | 500000 | 0 | Active |
| Bob | 102x1x0 | 500000 | 0 | 500000 | Active |

Peer check: Alice lists Bob? [x]   Bob lists Alice? [x]

## Table 3 — Exercise 3 (multi-hop payment)

Channel balances before payment:

| Channel | Alice local (sat) | Bob local (sat) | Carol local (sat) | State |
|---------|-------------------|-----------------|-------------------|-------|
| Alice→Bob | | | | |
| Bob→Carol | | | | |

Invoice: inv-ex3, 100,000 sat, payee = Carol

| Item | Value |
|------|-------|
| Payment status (Alice listpays) | complete |
| Preimage received? | [ ] |
| Invoice paid (Carol listinvoices)? | [ ] |
| Alice→Bob: Alice local change | -100,000 (-fee) |
| Bob→Carol: Bob local change, fee collected | |

## Table 4 — Exercise 4 (circular rebalance)

Setup: Alice→Bob (Alice funded), Bob→Carol (Bob funded), Carol→Alice (Carol funded)

| Channel | Local bal BEFORE (sat) | Local bal AFTER (sat) | Change (sat) |
|---------|------------------------|-----------------------|--------------|
| Alice→Bob (Alice side) | | | ≈ -150,000 |
| Bob→Carol (Bob side) | | | ≈ -150,000 (-fee) |
| Carol→Alice (Carol side) | | | ≈ -150,000 |
| Carol→Alice (Alice remote side) | | | ≈ +150,000 |

| Item | Value |
|------|-------|
| Payment status (Alice listpays) | complete |
| Preimage received? | [ ] |
| Invoice inv-ex4 paid (Carol)? | [ ] |
| All 3 channels CHANNELD_NORMAL? | [ ] |

Notes (routing fees observed, anything unexpected):
