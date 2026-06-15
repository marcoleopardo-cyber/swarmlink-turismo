import 'package:flutter/material.dart';
import 'package:geolocator/geolocator.dart';

class SwarmProvider extends ChangeNotifier {
  String connectionStatus = 'Inizializzazione Swarm...';
  String bestRoute = 'Satellite D2D';
  List<String> nearbyPeers = [];
  double signalStrength = 85.0;
  bool isLiFiAvailable = false;
  bool isDataEncrypted = true; // Simulazione crittografia E2EE
  String encryptionStatus = 'E2EE Attivo (AES-256 + ChaCha20)';

  SwarmProvider() {
    _initializeSwarm();
  }

  Future<void> _initializeSwarm() async {
    // Simulazione GPS
    try {
      await Geolocator.checkPermission();
      Position position = await Geolocator.getCurrentPosition();
      print('Posizione turistica: ${position.latitude}, ${position.longitude}');
    } catch (e) {
      print('GPS simulato per demo');
    }

    // Simulazione discovery
    await Future.delayed(const Duration(seconds: 2));
    nearbyPeers = ['Turista1 - Roma', 'Turista2 - Firenze', 'Escursionista - Montagne'];
    bestRoute = nearbyPeers.isNotEmpty ? 'Mesh Locale (Bassa Latenza)' : 'Satellite Starlink DTC';
    connectionStatus = 'Swarm Attivo (${nearbyPeers.length} turisti vicini)';
    signalStrength = 92.0;
    isLiFiAvailable = true;

    notifyListeners();
  }

  void refreshSwarm() {
    connectionStatus = 'Rilettura Swarm...';
    notifyListeners();
    _initializeSwarm();
  }

  void toggleLiFi() {
    isLiFiAvailable = !isLiFiAvailable;
    notifyListeners();
  }

  // Simulazione Crittografia Avanzata
  String simulateEncryption(String message) {
    return '[E2EE] ${message.hashCode} - Crittografato con AES-256 + ChaCha20-Poly1305';
  }

  void refreshEncryption() {
    isDataEncrypted = true;
    encryptionStatus = 'E2EE Attivo (chiave temporanea rigenerata)';
    notifyListeners();
  }
}
