ParkPredict 2.0 — Requirements Traceability Matrix
====================================================

Requirement (R#)          -> Where implemented (solution.py functions/classes)      -> Test cases
----------------------------------------------------------------------------------------------------
R1  Multi-location system -> LOCATIONS (5 sites), Space, ParkingLot.add_location    -> TestParking.test_multi_location_isolation
R2  Smart dashboard       -> ParkingLot.stats() occupancy %, peak-hour analysis      -> TestParking.test_dashboard_stats, TestDemand.test_peak_multiplier
R3  Early release         -> ParkingLot.vacate(), waiter notification, auto-claim    -> TestVacate.test_vacate_frees_slot, .test_vacate_notifies_waiter, .test_vacate_auto_claims_waiter
R4  AI prediction         -> DemandForecaster.forecast, predict_release_probability  -> TestDemand.test_forecast_shape, .test_release_probability_bounds, .test_wait_time_consistent
R5  Reservations          -> ParkingLot.reserve_slot / cancel_reservation lifecycle  -> TestReservation.test_reserve_and_cancel, .test_double_reserve_rejected, .test_expired_reservation
R6  Mall mode             -> MallConfig + ParkingLot(fee_calculator=MallFee)         -> TestPricing.test_mall_fee_visitor_premium
R7  Indoor navigation     -> Space.floor/zone/dist, route_to_slot                    -> TestNavigation.test_route_returns_steps
R8  Find My Car           -> ParkingLot.save_find_car / find_car                     -> TestFindCar.test_save_and_find
R9  Smart allocation      -> ParkingLot.find_best_slot (ETA x prob x risk score)     -> TestAllocation.test_best_slot_prefers_free_and_near, .test_ev_car_gets_ev_slot
R10 EV management         -> EVStation.charge_tick, ParkingLot.start_charging        -> TestEV.test_charging_progresses, .test_charge_completes
R11 Dynamic pricing       -> FeeCalculator (base x peak x role x EV, rain surcharge) -> TestPricing.test_base_fee, .test_peak_surcharge, .test_visitor_premium, .test_rain_surge, .test_ev_energy
R12 Admin command centre  -> ParkingLot.report(), collect_alerts                     -> TestAdmin.test_report_totals, .test_overstay_alert
R13 Smart notifications   -> ParkingLot._notify (event log), VacateEvent payloads    -> TestVacate.test_vacate_notifies_waiter
R14 Modern UI             -> parkpredict-2.0.html (web client, out of py scope)      -> visual / Lighthouse 100 x4
R15 Technical hygiene     -> unittest suite embedded; seeded RNG reproducibility     -> entire TestSeed reproducibility test
