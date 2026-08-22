# FOR-YOU-CHEEKU-
import React, { useState, useEffect, useRef } from 'react';
import {
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
  Animated,
  Easing,
  Dimensions,
  TextInput,
  ScrollView,
  SafeAreaView,
  StatusBar,
  KeyboardAvoidingView,
  Platform,
} from 'react-native';
import AsyncStorage from '@react-native-async-storage/async-storage';
import * as Haptics from 'expo-haptics';
import { Heart, Gift, Frown, Sparkles, ChevronLeft, Send, Lock } from 'lucide-react-native';

const { width, height } = Dimensions.get('window');

// ============================================================================
// CONFIGURATION & CUSTOMIZABLE DATA
// ============================================================================
const ROMANTIC_MESSAGES = [
  "I love you.",
  "You are my favourite person.",
  "I would still choose you.",
  "You make ordinary days feel special.",
  "I hope you never forget how loved you are.",
  "I love having you in my life.",
  "You make my world a little better.",
  "I don't need a perfect life. I just want you in mine.",
  "You are one of the best things that ever happened to me.",
  "And if you ask me why I love you... I probably won't know how to explain it.",
  "My favorite place in the world is right next to you.",
  "You have no idea how much my heart races when I see you smile."
];

const APOLOGY_TEXT = 
  "I know I don't always get everything right.\n" +
  "Sometimes I say things I shouldn't.\n" +
  "Sometimes I hurt you without meaning to.\n" +
  "But I'm genuinely sorry.\n" +
  "You mean too much to me to let my mistakes become bigger than us.";

const SURPRISES = [
  { id: '1', type: 'message', content: "I just wanted to remind you that I love you. ❤️", locked: false },
  { id: '2', type: 'hug', content: "If I could give you one thing right now, it would be a really long hug. 🤗", locked: false },
  { id: '3', type: 'compliment', content: "You're still my favourite person. In every universe.", locked: false },
  { id: '4', type: 'reminder', content: "Just a reminder: someone out here is thinking about you right now.", locked: false },
  { id: '5', type: 'simple', content: "Nothing special today...\n\nExcept that I love you.", locked: false },
  { id: '6', type: 'memory', content: "Remember when we first met? I knew right then you were special.", locked: false },
  { id: '7', type: 'future', content: "Something special is waiting here... [Locked Secret Surprise]", locked: true }
];

// Helper for haptics
const triggerHaptic = () => {
  if (Platform.OS !== 'web') {
    Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Light).catch(() => {});
  }
};

// ============================================================================
// COMPONENT: PARTICLE SYSTEM (FLOATING HEARTS)
// ============================================================================
const HeartParticle = ({ onAnimationEnd }) => {
  const animY = useRef(new Animated.Value(0)).current;
  const animOpacity = useRef(new Animated.Value(1)).current;
  const randomX = useRef((Math.random() - 0.5) * 160).current;
  const randomSize = useRef(14 + Math.random() * 12).current;

  useEffect(() => {
    Animated.parallel([
      Animated.timing(animY, {
        toValue: -120 - Math.random() * 50,
        duration: 1200 + Math.random() * 400,
        easing: Easing.out(Easing.quad),
        useNativeDriver: true,
      }),
      Animated.timing(animOpacity, {
        toValue: 0,
        duration: 1400,
        easing: Easing.linear,
        useNativeDriver: true,
      }),
    ]).start(() => {
      if (onAnimationEnd) onAnimationEnd();
    });
  }, []);

  return (
    <Animated.View
      style={{
        position: 'absolute',
        transform: [{ translateX: randomX }, { translateY: animY }],
        opacity: animOpacity,
      }}
    >
      <Heart size={randomSize} color="#FF6B81" fill="#FF6B81" />
    </Animated.View>
  );
};

// ============================================================================
// MAIN APP COMPONENT
// ============================================================================
export default function App() {
  const [currentScreen, setCurrentScreen] = useState('splash'); // splash, home, love, sorry, measure, surprise
  const [particles, setParticles] = useState([]);

  // --- SPLASH SCREEN LOGIC ---
  const splashPulse = useRef(new Animated.Value(1)).current;
  const splashOpacity = useRef(new Animated.Value(1)).current;

  useEffect(() => {
    // Pulse animation for splash heart
    Animated.loop(
      Animated.sequence([
        Animated.timing(splashPulse, {
          toValue: 1.25,
          duration: 800,
          easing: Easing.inOut(Easing.ease),
          useNativeDriver: true,
        }),
        Animated.timing(splashPulse, {
          toValue: 1,
          duration: 800,
          easing: Easing.inOut(Easing.ease),
          useNativeDriver: true,
        }),
      ])
    ).start();

    // Auto-navigate to home
    const timer = setTimeout(() => {
      Animated.timing(splashOpacity, {
        toValue: 0,
        duration: 600,
        useNativeDriver: true,
      }).start(() => {
        setCurrentScreen('home');
      });
    }, 2800);

    return () => clearTimeout(timer);
  }, []);

  const spawnParticles = (count = 6) => {
    triggerHaptic();
    const newParticles = Array.from({ length: count }).map((_, i) => Date.now() + i);
    setParticles((prev) => [...prev, ...newParticles]);
  };

  const removeParticle = (id) => {
    setParticles((prev) => prev.filter((p) => p !== id));
  };

  // --- SCREEN RENDERERS ---
  const renderHeader = (title) => (
    <View style={styles.header}>
      <TouchableOpacity
        style={styles.backButton}
        onPress={() => {
          triggerHaptic();
          setCurrentScreen('home');
        }}
        activeOpacity={0.7}
      >
        <ChevronLeft size={20} color="#FF6B81" />
        <Text style={styles.backText}>For You</Text>
      </TouchableOpacity>
      <Text style={styles.headerTitle}>{title}</Text>
      <View style={{ width: 60 }} />
    </View>
  );

  return (
    <SafeAreaView style={styles.container}>
      <StatusBar barStyle="dark-content" backgroundColor="#FFF8F9" />

      {/* 1. SPLASH SCREEN */}
      {currentScreen === 'splash' && (
        <Animated.View style={[styles.splashContainer, { opacity: splashOpacity }]}>
          <Animated.View style={{ transform: [{ scale: splashPulse }] }}>
            <Heart size={80} color="#FF6B81" fill="#FF6B81" />
          </Animated.View>
          <Text style={styles.splashTitle}>For You</Text>
          <Text style={styles.splashSubtitle}>A little place made only for you.</Text>
        </Animated.View>
      )}

      {/* 2. HOME SCREEN */}
      {currentScreen === 'home' && (
        <View style={styles.mainContent}>
          <View style={styles.homeHeader}>
            <Text style={styles.mainTitle}>For You ❤️</Text>
            <Text style={styles.subTitle}>Select a card below</Text>
          </View>

          <View style={styles.menuGrid}>
            <TouchableOpacity
              style={styles.card}
              activeOpacity={0.85}
              onPress={() => {
                triggerHaptic();
                setCurrentScreen('love');
              }}
            >
              <View style={[styles.iconContainer, { backgroundColor: '#FFEBF0' }]}>
                <Heart size={28} color="#FF6B81" fill="#FF6B81" />
              </View>
              <Text style={styles.cardTitle}>I Love You</Text>
            </TouchableOpacity>

            <TouchableOpacity
              style={styles.card}
              activeOpacity={0.85}
              onPress={() => {
                triggerHaptic();
                setCurrentScreen('sorry');
              }}
            >
              <View style={[styles.iconContainer, { backgroundColor: '#FFF0F5' }]}>
                <Frown size={28} color="#FF8FA3" />
              </View>
              <Text style={styles.cardTitle}>I'm Sorry</Text>
            </TouchableOpacity>

            <TouchableOpacity
              style={styles.card}
              activeOpacity={0.85}
              onPress={() => {
                triggerHaptic();
                setCurrentScreen('measure');
              }}
            >
              <View style={[styles.iconContainer, { backgroundColor: '#FFF2F0' }]}>
                <Sparkles size={28} color="#FF758F" />
              </View>
              <Text style={styles.cardTitle}>How Much I Love You</Text>
            </TouchableOpacity>

            <TouchableOpacity
              style={styles.card}
              activeOpacity={0.85}
              onPress={() => {
                triggerHaptic();
                setCurrentScreen('surprise');
              }}
            >
              <View style={[styles.iconContainer, { backgroundColor: '#FFF5F5' }]}>
                <Gift size={28} color="#FF4D6D" />
              </View>
              <Text style={styles.cardTitle}>A Little Surprise</Text>
            </TouchableOpacity>
          </View>
        </View>
      )}

      {/* 3. FEATURE 1: I LOVE YOU */}
      {currentScreen === 'love' && (
        <ILoveYouScreen
          renderHeader={renderHeader}
          spawnParticles={spawnParticles}
          particles={particles}
          removeParticle={removeParticle}
        />
      )}

      {/* 4. FEATURE 2: I'M SORRY */}
      {currentScreen === 'sorry' && <ImSorryScreen renderHeader={renderHeader} />}

      {/* 5. FEATURE 3: HOW MUCH I LOVE YOU */}
      {currentScreen === 'measure' && <MeasureLoveScreen renderHeader={renderHeader} />}

      {/* 6. FEATURE 4: A LITTLE SURPRISE */}
      {currentScreen === 'surprise' && (
        <SurpriseScreen
          renderHeader={renderHeader}
          spawnParticles={spawnParticles}
          particles={particles}
          removeParticle={removeParticle}
        />
      )}
    </SafeAreaView>
  );
}

// ============================================================================
// SUB-SCREEN 1: I LOVE YOU
// ============================================================================
function ILoveYouScreen({ renderHeader, spawnParticles, particles, removeParticle }) {
  const [msgIndex, setMsgIndex] = useState(0);
  const heartScale = useRef(new Animated.Value(1)).current;
  const msgFade = useRef(new Animated.Value(1)).current;

  const handleTap = () => {
    spawnParticles(8);

    // Heart bounce
    Animated.sequence([
      Animated.timing(heartScale, { toValue: 1.3, duration: 150, useNativeDriver: true }),
      Animated.timing(heartScale, { toValue: 1, duration: 150, useNativeDriver: true }),
    ]).start();

    // Message transition
    Animated.timing(msgFade, { toValue: 0, duration: 150, useNativeDriver: true }).start(() => {
      let nextIdx;
      do {
        nextIdx = Math.floor(Math.random() * ROMANTIC_MESSAGES.length);
      } while (nextIdx === msgIndex && ROMANTIC_MESSAGES.length > 1);

      setMsgIndex(nextIdx);
      Animated.timing(msgFade, { toValue: 1, duration: 250, useNativeDriver: true }).start();
    });
  };

  return (
    <View style={styles.featureContainer}>
      {renderHeader("I Love You")}
      <View style={styles.centerContent}>
        <View style={styles.particleCanvas}>
          {particles.map((id) => (
            <HeartParticle key={id} onAnimationEnd={() => removeParticle(id)} />
          ))}
          <TouchableOpacity activeOpacity={0.9} onPress={handleTap}>
            <Animated.View style={{ transform: [{ scale: heartScale }] }}>
              <Heart size={110} color="#FF6B81" fill="#FF6B81" />
            </Animated.View>
          </TouchableOpacity>
        </View>

        <Text style={styles.tapInstruction}>Tap the heart</Text>

        <Animated.View style={[styles.messageCard, { opacity: msgFade }]}>
          <Text style={styles.messageText}>"{ROMANTIC_MESSAGES[msgIndex]}"</Text>
        </Animated.View>

        <Text style={styles.subInstruction}>Tap the heart again ❤️</Text>
      </View>
    </View>
  );
}

// ============================================================================
// SUB-SCREEN 2: I'M SORRY
// ============================================================================
function ImSorryScreen({ renderHeader }) {
  const [stage, setStage] = useState('initial'); // 'initial', 'apology', 'response'
  const [responseType, setResponseType] = useState(null); // 'yes', 'chat', 'angry'
  const [messages, setMessages] = useState([]);
  const [inputText, setInputText] = useState('');

  const handleSendMessage = () => {
    if (!inputText.trim()) return;
    triggerHaptic();
    setMessages((prev) => [...prev, { id: Date.now().toString(), text: inputText }]);
    setInputText('');
  };

  return (
    <KeyboardAvoidingView
      style={styles.featureContainer}
      behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
    >
      {renderHeader("I'm Sorry")}

      <ScrollView contentContainerStyle={styles.scrollContent} keyboardShouldPersistTaps="handled">
        {stage === 'initial' && (
          <View style={styles.centerContent}>
            <Frown size={70} color="#FF8FA3" style={{ marginBottom: 16 }} />
            <Text style={styles.sorryTitle}>I'm Sorry...</Text>
            <Text style={styles.sorrySubtitle}>I know sometimes I mess things up.</Text>

            <TouchableOpacity
              style={styles.primaryBtn}
              activeOpacity={0.8}
              onPress={() => {
                triggerHaptic();
                setStage('apology');
              }}
            >
              <Text style={styles.primaryBtnText}>Listen to me</Text>
            </TouchableOpacity>
          </View>
        )}

        {stage === 'apology' && (
          <View style={styles.apologyContainer}>
            <View style={styles.apologyCard}>
              <Text style={styles.apologyText}>{APOLOGY_TEXT}</Text>
            </View>

            <Text style={styles.forgiveQuestion}>Forgive me?</Text>

            <View style={styles.optionList}>
              <TouchableOpacity
                style={[styles.optionBtn, { backgroundColor: '#FFEBF0' }]}
                onPress={() => {
                  triggerHaptic();
                  setResponseType('yes');
                  setStage('response');
                }}
              >
                <Text style={styles.optionBtnText}>❤️ Yes</Text>
              </TouchableOpacity>

              <TouchableOpacity
                style={[styles.optionBtn, { backgroundColor: '#FFF5F7' }]}
                onPress={() => {
                  triggerHaptic();
                  setResponseType('chat');
                  setStage('response');
                }}
              >
                <Text style={styles.optionBtnText}>💬 Talk to me</Text>
              </TouchableOpacity>

              <TouchableOpacity
                style={[styles.optionBtn, { backgroundColor: '#F8F9FA' }]}
                onPress={() => {
                  triggerHaptic();
                  setResponseType('angry');
                  setStage('response');
                }}
              >
                <Text style={styles.optionBtnText}>😤 Still angry</Text>
              </TouchableOpacity>
            </View>
          </View>
        )}

        {stage === 'response' && (
          <View style={styles.responseContainer}>
            {responseType === 'yes' && (
              <View style={styles.centerContent}>
                <Heart size={80} color="#FF6B81" fill="#FF6B81" style={{ marginBottom: 20 }} />
                <Text style={styles.responseTitle}>Thank you ❤️</Text>
                <Text style={styles.responseSubtitle}>I promise I'll try to do better.</Text>
              </View>
            )}

            {responseType === 'angry' && (
              <View style={styles.centerContent}>
                <Frown size={80} color="#FF8FA3" style={{ marginBottom: 20 }} />
                <Text style={styles.responseTitle}>Okay... I understand.</Text>
                <Text style={styles.responseSubtitle}>I'm still here whenever you're ready. ❤️</Text>
              </View>
            )}

            {responseType === 'chat' && (
              <View style={styles.chatWrapper}>
                <Text style={styles.chatHeaderTitle}>Okay... I'm listening.</Text>
                <Text style={styles.chatHeaderSubtitle}>Tell me what's in your heart.</Text>

                <View style={styles.chatBox}>
                  {messages.length === 0 ? (
                    <Text style={styles.emptyChatText}>Type your thoughts below...</Text>
                  ) : (
                    messages.map((m) => (
                      <View key={m.id} style={styles.chatBubble}>
                        <Text style={styles.chatBubbleText}>{m.text}</Text>
                      </View>
                    ))
                  )}
                </View>

                <View style={styles.inputRow}>
                  <TextInput
                    style={styles.textInput}
                    placeholder="Write here..."
                    placeholderTextColor="#A0A0A0"
                    value={inputText}
                    onChangeText={setInputText}
                  />
                  <TouchableOpacity style={styles.sendBtn} onPress={handleSendMessage}>
                    <Send size={18} color="#FFF" />
                  </TouchableOpacity>
                </View>
              </View>
            )}
          </View>
        )}
      </ScrollView>
    </KeyboardAvoidingView>
  );
}

// ============================================================================
// SUB-SCREEN 3: HOW MUCH I LOVE YOU
// ============================================================================
function MeasureLoveScreen({ renderHeader }) {
  const [counter, setCounter] = useState(0);
  const [isCounting, setIsCounting] = useState(false);
  const [isFinished, setIsFinished] = useState(false);
  const pulseAnim = useRef(new Animated.Value(1)).current;

  const startMeasurement = () => {
    triggerHaptic();
    setCounter(0);
    setIsCounting(true);
    setIsFinished(false);

    let currentVal = 0;
    const interval = setInterval(() => {
      currentVal += Math.floor(Math.random() * 25) + 10;
      if (currentVal >= 999) {
        clearInterval(interval);
        setCounter('999');
        setTimeout(() => {
          setIsCounting(false);
          setIsFinished(true);
          // Start pulsating infinity
          Animated.loop(
            Animated.sequence([
              Animated.timing(pulseAnim, { toValue: 1.3, duration: 600, useNativeDriver: true }),
              Animated.timing(pulseAnim, { toValue: 1, duration: 600, useNativeDriver: true }),
            ])
          ).start();
        }, 500);
      } else {
        setCounter(currentVal);
      }
    }, 100);
  };

  return (
    <View style={styles.featureContainer}>
      {renderHeader("How Much I Love You")}
      <View style={styles.centerContent}>
        <Text style={styles.measureSubtitle}>Want to know how much I love you?</Text>

        {!isCounting && !isFinished && (
          <TouchableOpacity style={styles.primaryBtn} activeOpacity={0.8} onPress={startMeasurement}>
            <Text style={styles.primaryBtnText}>MEASURE MY LOVE ❤️</Text>
          </TouchableOpacity>
        )}

        {(isCounting || isFinished) && (
          <View style={styles.counterBox}>
            {!isFinished ? (
              <Text style={styles.counterText}>{counter}%</Text>
            ) : (
              <Animated.Text style={[styles.infinityText, { transform: [{ scale: pulseAnim }] }]}>
                ∞
              </Animated.Text>
            )}
          </View>
        )}

        {isFinished && (
          <View style={styles.finalMessageContainer}>
            <Text style={styles.finalTextMain}>There isn't a number big enough.</Text>
            <Text style={styles.finalTextSub}>So I stopped counting.</Text>

            <TouchableOpacity
    
