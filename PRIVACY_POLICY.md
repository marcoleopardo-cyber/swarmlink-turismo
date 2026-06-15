import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'screens/dashboard_screen.dart';
import 'providers/swarm_provider.dart';

void main() {
  runApp(const SwarmLinkTurismoApp());
}

class SwarmLinkTurismoApp extends StatelessWidget {
  const SwarmLinkTurismoApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MultiProvider(
      providers: [
        ChangeNotifierProvider(create: (_) => SwarmProvider()),
      ],
      child: MaterialApp(
        title: 'SwarmLink Turismo',
        theme: ThemeData(
          primarySwatch: Colors.blue,
          useMaterial3: true,
        ),
        home: const DashboardScreen(),
        debugShowCheckedModeBanner: false,
      ),
    );
  }
}
