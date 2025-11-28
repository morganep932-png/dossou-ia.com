<!-- The exported code uses Tailwind CSS. Install Tailwind CSS in your dev environment to ensure all styles work. -->
<template>
<div class="min-h-screen bg-gradient-to-br from-amber-50 to-orange-100">
<!-- Header -->
<header class="bg-white shadow-lg border-b-4 border-amber-400">
<div class="max-w-7xl mx-auto px-6 py-4">
<div class="flex items-center justify-between">
<div class="flex items-center space-x-4">
<div class="w-16 h-16 bg-gradient-to-br from-amber-600 to-orange-700 rounded-full flex items-center justify-center overflow-hidden">
<img
src="https://readdy.ai/api/search-image?query=majestic%20african%20king%20wearing%20golden%20crown%20sitting%20on%20ornate%20throne%20with%20traditional%20african%20patterns%20and%20royal%20regalia%20against%20warm%20golden%20background&width=64&height=64&seq=logo001&orientation=squarish"
alt="Logo Dossou"
class="w-full h-full object-cover"
/>
</div>
<h1 class="text-3xl font-bold text-amber-800">Dossou</h1>
</div>
<nav class="hidden md:flex space-x-8">
<a href="#" class="text-gray-700 hover:text-amber-600 font-medium cursor-pointer">Accueil</a>
<a href="#bibliotheque" class="text-gray-700 hover:text-amber-600 font-medium cursor-pointer">Bibliothèque</a>
<a href="#musique" @click="scrollToMusic" class="text-gray-700 hover:text-amber-600 font-medium cursor-pointer">Musique</a>
<a href="#abonnements" @click="scrollToSubscriptions" class="text-gray-700 hover:text-amber-600 font-medium cursor-pointer">Abonnements</a>
<a href="#" @click="openAccountModal" class="text-gray-700 hover:text-amber-600 font-medium cursor-pointer">Mon Compte</a>
</nav>
<div v-if="isLoggedIn" class="flex items-center space-x-4">
<div class="bg-amber-100 text-amber-800 px-3 py-1 rounded-full text-sm font-medium">
<i class="fas fa-coins mr-1"></i>{{ userCredits }} crédits
</div>
<span class="text-gray-700">{{ loginInfo.firstName }}</span>
<button @click="logout" class="text-gray-600 hover:text-amber-600 cursor-pointer">
<i class="fas fa-sign-out-alt"></i>
</button>
</div>
<button v-else @click="openLoginModal" class="bg-amber-600 text-white px-6 py-2 !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer">
Se connecter
</button>
</div>
</div>
</header>
<!-- Hero Section -->
<section class="relative min-h-96 bg-gradient-to-r from-amber-900 via-orange-800 to-red-900 overflow-hidden">
<div class="absolute inset-0">
<img
src="https://readdy.ai/api/search-image?query=epic%20african%20landscape%20with%20ancient%20kingdoms%20and%20golden%20sunset%20showcasing%20traditional%20architecture%20baobab%20trees%20and%20vast%20savanna%20with%20warm%20golden%20lighting%20perfect%20for%20text%20overlay&width=1440&height=600&seq=hero001&orientation=landscape"
alt="Histoire Africaine"
class="w-full h-full object-cover object-top opacity-40"
/>
</div>
<div class="relative max-w-7xl mx-auto px-6 py-24">
<div class="grid md:grid-cols-2 gap-12 items-center">
<div class="text-white">
<h2 class="text-5xl font-bold mb-6 leading-tight">
Découvrez l'Histoire Africaine en Vidéos 4K
</h2>
<p class="text-xl mb-8 text-amber-100">
Générez des vidéos haute définition sur l'histoire africaine grâce à nos prompts intelligents.
Explorez les royaumes, les héros et les civilisations qui ont façonné notre continent.
Partagez directement sur TikTok, Facebook, Instagram et YouTube.
</p>
<button @click="startJourney" class="bg-amber-500 text-white px-8 py-4 text-lg font-semibold !rounded-button hover:bg-amber-600 transition-colors whitespace-nowrap cursor-pointer">
Commencer votre voyage
</button>
</div>
</div>
</div>
</section>
<!-- Music Composition Section -->
<section class="py-16 bg-gradient-to-br from-purple-50 to-indigo-50">
<div class="max-w-7xl mx-auto px-6">
<h3 class="text-3xl font-bold text-center mb-8 text-gray-800">
Composition Musicale Africaine
</h3>
<p class="text-center text-gray-600 mb-12 max-w-2xl mx-auto">
Transformez vos textes en compositions musicales authentiques avec des styles africains traditionnels et modernes. Créez des mélodies uniques inspirées de la richesse musicale du continent.
</p>
<div class="bg-white rounded-xl shadow-lg p-8 border-2 border-purple-200 max-w-4xl mx-auto">
<!-- Text Input -->
<div class="mb-6">
<label class="block text-sm font-medium text-gray-700 mb-2">
Votre texte à transformer en musique
</label>
<textarea
v-model="musicText"
class="w-full h-32 p-4 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent resize-none"
placeholder="Ex: L'histoire de nos ancêtres résonne dans le vent, leurs voix chantent encore dans nos cœurs..."
maxlength="500"
></textarea>
<div class="text-right text-xs text-gray-500 mt-1">
{{ musicText.length }}/500 caractères
</div>
</div>
<!-- Music Style Selection -->
<div class="mb-6">
<label class="block text-sm font-medium text-gray-700 mb-4">Style musical</label>
<div class="grid md:grid-cols-3 lg:grid-cols-4 gap-4">
<div v-for="style in musicStyles" :key="style.name"
@click="selectedMusicStyle = style.name"
class="p-4 border-2 rounded-lg cursor-pointer hover:bg-gray-50 transition-colors"
:class="{ 'border-purple-500 bg-purple-50': selectedMusicStyle === style.name, 'border-gray-200': selectedMusicStyle !== style.name }">
<div class="text-center">
<div class="w-12 h-12 mx-auto mb-2 flex items-center justify-center rounded-full"
:style="{ backgroundColor: style.color + '20' }">
<i :class="style.icon" class="text-2xl" :style="{ color: style.color }"></i>
</div>
<h4 class="font-semibold text-gray-800 text-sm">{{ style.name }}</h4>
<p class="text-xs text-gray-600 mt-1">{{ style.origin }}</p>
</div>
</div>
</div>
</div>
<!-- Music Parameters -->
<div class="grid md:grid-cols-3 gap-6 mb-6">
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">Tempo</label>
<select v-model="musicTempo" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500">
<option value="lent">Lent (60-80 BPM)</option>
<option value="modéré">Modéré (80-120 BPM)</option>
<option value="rapide">Rapide (120-160 BPM)</option>
<option value="très rapide">Très rapide (160+ BPM)</option>
</select>
</div>
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">Durée</label>
<select v-model="musicDuration" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500">
<option value="30s">30 secondes</option>
<option value="1min">1 minute</option>
<option value="2min">2 minutes</option>
<option value="3min">3 minutes</option>
</select>
</div>
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">Instruments principaux</label>
<select v-model="musicInstruments" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500">
<option value="traditionnel">Instruments traditionnels</option>
<option value="moderne">Instruments modernes</option>
<option value="mixte">Mélange traditionnel/moderne</option>
</select>
</div>
</div>
<!-- Generation Button -->
<button
@click="generateMusic"
class="w-full bg-purple-600 text-white py-4 font-semibold !rounded-button hover:bg-purple-700 transition-colors whitespace-nowrap cursor-pointer"
:disabled="!musicText.trim() || (!isLoggedIn || userCredits === 0)"
:class="{ 'opacity-50 cursor-not-allowed': !musicText.trim() || (!isLoggedIn || userCredits === 0) }"
>
<i class="fas fa-music mr-2"></i>
<span v-if="!isLoggedIn">Se connecter pour composer</span>
<span v-else-if="userCredits === 0">Plus de crédits - S'abonner</span>
<span v-else>Composer ma musique (1 crédit)</span>
</button>
</div>
<!-- Generated Music Gallery -->
<div v-if="generatedMusics.length > 0" class="mt-12">
<h4 class="text-2xl font-bold text-center mb-8 text-gray-800">
Compositions Musicales Récentes
</h4>
<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
<div v-for="music in generatedMusics" :key="music.id" class="bg-white rounded-lg shadow-lg overflow-hidden hover:shadow-xl transition-shadow cursor-pointer">
<div class="relative">
<div class="h-48 bg-gradient-to-br flex items-center justify-center"
:style="{ background: `linear-gradient(135deg, ${music.style.color}20, ${music.style.color}40)` }">
<div class="text-center">
<i :class="music.style.icon" class="text-6xl mb-4" :style="{ color: music.style.color }"></i>
<h5 class="text-lg font-bold text-gray-800">{{ music.style.name }}</h5>
<p class="text-sm text-gray-600">{{ music.style.origin }}</p>
</div>
</div>
<button @click="playMusic(music)" class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 bg-white bg-opacity-90 hover:bg-opacity-100 rounded-full p-4 cursor-pointer">
<i class="fas fa-play text-purple-600 text-2xl"></i>
</button>
<div class="absolute bottom-2 right-2 bg-black bg-opacity-75 text-white px-2 py-1 text-xs rounded">
{{ music.duration }}
</div>
</div>
<div class="p-4">
<h4 class="font-semibold text-gray-800 mb-2">{{ music.title }}</h4>
<p class="text-sm text-gray-600 mb-3 line-clamp-2">{{ music.description }}</p>
<div class="flex items-center justify-between mb-3">
<span class="text-xs bg-purple-100 text-purple-800 px-2 py-1 rounded">{{ music.tempo }}</span>
<span class="text-xs text-gray-500">{{ music.instruments }}</span>
</div>
<div class="flex space-x-2">
<button @click="downloadMusic(music)" class="flex-1 bg-purple-600 text-white py-2 px-3 !rounded-button hover:bg-purple-700 transition-colors cursor-pointer text-sm whitespace-nowrap">
<i class="fas fa-download mr-1"></i>MP3
</button>
<button @click="shareMusic(music)" class="flex-1 bg-gray-600 text-white py-2 px-3 !rounded-button hover:bg-gray-700 transition-colors cursor-pointer text-sm whitespace-nowrap">
<i class="fas fa-share mr-1"></i>Partager
</button>
</div>
</div>
</div>
</div>
</div>
</div>
</section>
<!-- Video Gallery -->
<section class="py-16 bg-white">
<div class="max-w-7xl mx-auto px-6">
<h3 class="text-3xl font-bold text-center mb-12 text-gray-800">
Vidéos Historiques Récemment Générées
</h3>
<div class="grid md:grid-cols-3 lg:grid-cols-4 gap-6">
<div v-for="video in videos" :key="video.id" class="bg-white rounded-lg shadow-lg overflow-hidden hover:shadow-xl transition-shadow cursor-pointer">
<div class="relative">
<img
:src="video.thumbnail"
:alt="video.title"
class="w-full h-48 object-cover object-top"
/>
<div class="absolute top-2 right-2 bg-red-600 text-white px-2 py-1 text-xs font-bold rounded">
4K
</div>
<div class="absolute bottom-2 right-2 bg-black bg-opacity-75 text-white px-2 py-1 text-xs rounded">
{{ video.duration }}
</div>
<button @click="openVideoModal(video)" class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 bg-white bg-opacity-90 hover:bg-opacity-100 rounded-full p-3 cursor-pointer">
<i class="fas fa-play text-amber-600 text-xl"></i>
</button>
</div>
<div class="p-4">
<h4 class="font-semibold text-gray-800 mb-2">{{ video.title }}</h4>
<p class="text-sm text-gray-600 mb-3">{{ video.description }}</p>
<div class="flex justify-between items-center">
<div class="flex space-x-2">
<button class="bg-pink-500 text-white p-2 rounded !rounded-button hover:bg-pink-600 transition-colors cursor-pointer" title="Partager sur TikTok">
<i class="fab fa-tiktok text-sm"></i>
</button>
<button class="bg-blue-600 text-white p-2 rounded !rounded-button hover:bg-blue-700 transition-colors cursor-pointer" title="Partager sur Facebook">
<i class="fab fa-facebook text-sm"></i>
</button>
<button class="bg-gradient-to-r from-purple-500 to-pink-500 text-white p-2 rounded !rounded-button hover:from-purple-600 hover:to-pink-600 transition-colors cursor-pointer" title="Partager sur Instagram">
<i class="fab fa-instagram text-sm"></i>
</button>
<button class="bg-red-600 text-white p-2 rounded !rounded-button hover:bg-red-700 transition-colors cursor-pointer" title="Partager sur YouTube">
<i class="fab fa-youtube text-sm"></i>
</button>
</div>
<span class="text-xs text-gray-500">{{ video.shares }} partages</span>
</div>
</div>
</div>
</div>
</div>
</section>
<!-- Prompt Library -->
<section id="bibliotheque" class="py-16 bg-gradient-to-br from-amber-50 to-orange-50">
<div class="max-w-7xl mx-auto px-6">
<h3 class="text-3xl font-bold text-center mb-8 text-gray-800">
Bibliothèque de Prompts Historiques
</h3>
<p class="text-center text-gray-600 mb-12 max-w-2xl mx-auto">
Découvrez notre collection de prompts soigneusement conçus pour générer des vidéos captivantes sur l'histoire africaine. Chaque prompt est optimisé pour créer du contenu viral sur les réseaux sociaux.
</p>
<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
<div v-for="promptExample in promptLibrary" :key="promptExample.id" class="bg-white rounded-xl shadow-lg p-6 hover:shadow-xl transition-shadow cursor-pointer">
<div class="flex items-start justify-between mb-4">
<div class="flex items-center space-x-3">
<div class="w-12 h-12 bg-gradient-to-br from-amber-500 to-orange-600 rounded-full flex items-center justify-center">
<i :class="promptExample.icon" class="text-white text-xl"></i>
</div>
<div>
<h4 class="font-bold text-gray-800">{{ promptExample.category }}</h4>
<span class="text-xs bg-green-100 text-green-800 px-2 py-1 rounded-full">{{ promptExample.difficulty }}</span>
</div>
</div>
<div class="flex space-x-1">
<span v-for="platform in promptExample.bestPlatforms" :key="platform"
@click="usePrompt(promptExample, platform)"
class="text-xs bg-blue-100 text-blue-800 px-2 py-1 rounded cursor-pointer hover:bg-blue-200 transition-colors">{{ platform }}</span>
</div>
</div>
<h5 class="font-semibold text-gray-800 mb-2">{{ promptExample.title }}</h5>
<p class="text-sm text-gray-600 mb-4 line-clamp-3">{{ promptExample.prompt }}</p>
<div class="flex items-center justify-between mb-4">
<div class="flex items-center space-x-4 text-xs text-gray-500">
<span><i class="fas fa-eye mr-1"></i>{{ promptExample.views }}</span>
<span><i class="fas fa-heart mr-1"></i>{{ promptExample.likes }}</span>
<span><i class="fas fa-share mr-1"></i>{{ promptExample.shares }}</span>
</div>
<span class="text-xs bg-amber-100 text-amber-800 px-2 py-1 rounded">{{ promptExample.duration }}</span>
</div>
<div class="flex space-x-2">
<button
@click="usePrompt(promptExample)"
class="flex-1 bg-amber-600 text-white py-2 px-4 !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer text-sm font-medium"
>
<i class="fas fa-video mr-2"></i>Utiliser
</button>
<button class="bg-gray-100 text-gray-600 p-2 !rounded-button hover:bg-gray-200 transition-colors cursor-pointer">
<i class="fas fa-bookmark"></i>
</button>
</div>
</div>
</div>
</div>
</section>
<!-- Prompt Generator -->
<section id="generator" class="py-16 bg-white">
<div class="max-w-4xl mx-auto px-6">
<h3 class="text-3xl font-bold text-center mb-8 text-gray-800">
Générateur de Vidéos par Prompts
</h3>
<div class="bg-white rounded-xl shadow-lg p-8 border-2 border-amber-200">
<div class="mb-6">
<label class="block text-sm font-medium text-gray-700 mb-2">
Décrivez l'histoire africaine que vous souhaitez voir en vidéo
</label>
<textarea
v-model="promptText"
class="w-full h-32 p-4 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent resize-none"
placeholder="Ex: L'empire du Mali au 14ème siècle, Mansa Moussa et sa richesse légendaire..."
></textarea>
</div>
<div class="grid md:grid-cols-3 gap-6 mb-6">
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">Style de vidéo</label>
<select v-model="selectedStyle" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500">
<option value="4k">Vidéo 4K réaliste</option>
<option value="animation">Dessin animé africain</option>
</select>
</div>
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">Format de vidéo</label>
<select v-model="selectedFormat" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500">
<option value="vertical">Vertical (TikTok, Instagram Reels)</option>
<option value="horizontal">Horizontal (YouTube, Facebook)</option>
<option value="square">Carré (Instagram Post)</option>
</select>
</div>
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">Durée souhaitée</label>
<select v-model="selectedDuration" class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500">
<option value="15s">15 secondes (TikTok)</option>
<option value="30s">30 secondes (Instagram)</option>
<option value="60s">1 minute (Facebook)</option>
<option value="3min">3 minutes (YouTube)</option>
</select>
</div>
</div>
<div class="mb-6">
<label class="block text-sm font-medium text-gray-700 mb-3">Plateformes de partage automatique</label>
<div class="grid grid-cols-2 md:grid-cols-4 gap-3">
<label v-for="platform in socialPlatforms" :key="platform.name" class="flex items-center space-x-2 p-3 border border-gray-200 rounded-lg hover:bg-gray-50 cursor-pointer">
<input
type="checkbox"
v-model="selectedPlatforms"
:value="platform.name"
class="rounded text-amber-600 focus:ring-amber-500"
>
<i :class="platform.icon" :style="{ color: platform.color }" class="text-xl"></i>
<span class="text-sm font-medium">{{ platform.name }}</span>
</label>
</div>
</div>
<div v-if="!isLoggedIn" class="bg-amber-50 border border-amber-200 rounded-lg p-4 mb-4">
<div class="flex items-center space-x-2 text-amber-800">
<i class="fas fa-info-circle"></i>
<p class="font-medium">Connectez-vous pour générer des vidéos gratuites</p>
</div>
<p class="text-amber-700 text-sm mt-1">
Bénéficiez de 2 crédits gratuits pour créer vos premières vidéos de 30 secondes avec le filigrane Dossou
</p>
</div>
<div v-if="isLoggedIn && userCredits === 0" class="bg-red-50 border border-red-200 rounded-lg p-4 mb-4">
<div class="flex items-center space-x-2 text-red-800">
<i class="fas fa-exclamation-triangle"></i>
<p class="font-medium">Plus de crédits disponibles</p>
</div>
<p class="text-red-700 text-sm mt-1">
Souscrivez à un abonnement pour générer des vidéos illimitées en 4K sans filigrane
</p>
</div>
<button
@click="generateVideo"
class="w-full bg-amber-600 text-white py-4 font-semibold !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer"
:disabled="!promptText.trim() || (!isLoggedIn || userCredits === 0)"
:class="{ 'opacity-50 cursor-not-allowed': !promptText.trim() || (!isLoggedIn || userCredits === 0) }"
>
<i class="fas fa-video mr-2"></i>
<span v-if="!isLoggedIn">Se connecter pour générer</span>
<span v-else-if="userCredits === 0">Plus de crédits - S'abonner</span>
<span v-else>
{{ selectedStyle === '4k' ? 'Générer ma vidéo 4K avec filigrane (1 crédit)' : 'Générer mon dessin animé avec filigrane (1 crédit)' }}
</span>
</button>
</div>
</div>
</section>
<!-- Subscription Plans -->
<section id="abonnements" class="py-16 bg-gradient-to-br from-amber-50 to-orange-100">
<div class="max-w-6xl mx-auto px-6">
<h3 class="text-3xl font-bold text-center mb-12 text-gray-800">
Choisissez votre Abonnement
</h3>
<div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
<div class="bg-gradient-to-br from-amber-50 to-orange-50 rounded-xl shadow-lg p-8 border-2 border-amber-200">
<h4 class="text-2xl font-bold text-amber-800 mb-4">Abonnement Mensuel</h4>
<div class="text-4xl font-bold text-amber-600 mb-6">
20 €<span class="text-lg text-gray-600">/mois</span>
</div>
<ul class="space-y-3 mb-8">
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Génération illimitée de vidéos</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Qualité 4K Ultra HD</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Prompts personnalisés</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Partage automatique sur réseaux sociaux</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Support prioritaire</span>
</li>
</ul>
<button @click="selectSubscriptionPlan('monthly')" class="w-full bg-amber-600 text-white py-3 font-semibold !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer">
Choisir ce plan
</button>
</div>
<div class="bg-gradient-to-br from-orange-50 to-red-50 rounded-xl shadow-lg p-8 border-2 border-orange-300 relative">
<div class="absolute -top-3 left-1/2 transform -translate-x-1/2 bg-orange-500 text-white px-4 py-1 rounded-full text-sm font-semibold">
Économisez 17%
</div>
<h4 class="text-2xl font-bold text-orange-800 mb-4">Abonnement Annuel</h4>
<div class="text-4xl font-bold text-orange-600 mb-6">
200 €<span class="text-lg text-gray-600">/an</span>
</div>
<ul class="space-y-3 mb-8">
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Génération illimitée de vidéos</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Qualité 4K Ultra HD</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Prompts personnalisés</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Partage automatique sur réseaux sociaux</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Support prioritaire</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Accès anticipé aux nouvelles fonctionnalités</span>
</li>
<li class="flex items-center">
<i class="fas fa-check text-green-500 mr-3"></i>
<span>Analytics avancées des réseaux sociaux</span>
</li>
</ul>
<button @click="selectSubscriptionPlan('yearly')" class="w-full bg-orange-600 text-white py-3 font-semibold !rounded-button hover:bg-orange-700 transition-colors whitespace-nowrap cursor-pointer">
Choisir ce plan
</button>
</div>
</div>
</div>
</section>
<!-- Payment Methods -->
<section class="py-16 bg-white">
<div class="max-w-4xl mx-auto px-6">
<h3 class="text-3xl font-bold text-center mb-12 text-gray-800">
Méthodes de Paiement Mobile
</h3>
<div class="grid md:grid-cols-4 gap-6">
<div v-for="payment in paymentMethods" :key="payment.name" class="bg-white rounded-lg shadow-lg p-6 text-center hover:shadow-xl transition-shadow cursor-pointer">
<div class="w-16 h-16 mx-auto mb-4 flex items-center justify-center">
<i :class="payment.icon" class="text-4xl" :style="{ color: payment.color }"></i>
</div>
<h4 class="font-semibold text-gray-800 mb-2">{{ payment.name }}</h4>
<p class="text-sm text-gray-600 mb-4">{{ payment.description }}</p>
<button class="w-full bg-gray-800 text-white py-2 !rounded-button hover:bg-gray-900 transition-colors whitespace-nowrap cursor-pointer">
Sélectionner
</button>
</div>
</div>
</div>
</section>
<!-- Testimonials -->
<section class="py-16 bg-gradient-to-br from-gray-50 to-gray-100">
<div class="max-w-6xl mx-auto px-6">
<h3 class="text-3xl font-bold text-center mb-12 text-gray-800">
Ce que disent nos utilisateurs
</h3>
<div class="grid md:grid-cols-3 gap-8">
<div v-for="testimonial in testimonials" :key="testimonial.id" class="bg-white rounded-lg p-6 shadow-lg">
<div class="flex items-center mb-4">
<img
:src="testimonial.avatar"
:alt="testimonial.name"
class="w-12 h-12 rounded-full object-cover mr-4"
/>
<div>
<h4 class="font-semibold text-gray-800">{{ testimonial.name }}</h4>
<p class="text-sm text-gray-600">{{ testimonial.role }}</p>
</div>
</div>
<p class="text-gray-700 italic">"{{ testimonial.comment }}"</p>
<div class="flex mt-3">
<i v-for="n in 5" :key="n" class="fas fa-star text-amber-400"></i>
</div>
</div>
</div>
</div>
</section>
<!-- Footer -->
<footer class="bg-gray-900 text-white py-12">
<div class="max-w-7xl mx-auto px-6">
<div class="grid md:grid-cols-4 gap-8">
<div>
<div class="flex items-center space-x-3 mb-4">
<div class="w-12 h-12 bg-gradient-to-br from-amber-600 to-orange-700 rounded-full flex items-center justify-center overflow-hidden">
<img
src="https://readdy.ai/api/search-image?query=majestic%20african%20king%20wearing%20golden%20crown%20sitting%20on%20ornate%20throne%20with%20traditional%20african%20patterns%20and%20royal%20regalia%20against%20warm%20golden%20background&width=48&height=48&seq=logo002&orientation=squarish"
alt="Logo Dossou"
class="w-full h-full object-cover"
/>
</div>
<h4 class="text-xl font-bold">Dossou</h4>
</div>
<p class="text-gray-400">
Votre plateforme de référence pour découvrir l'histoire africaine en vidéos 4K générées par IA et partagées sur les réseaux sociaux.
</p>
</div>
<div>
<h5 class="font-semibold mb-4">Plateforme</h5>
<ul class="space-y-2 text-gray-400">
<li><a href="#" @click="scrollToTop" class="hover:text-white cursor-pointer">Accueil</a></li>
<li><a href="#bibliotheque" class="hover:text-white cursor-pointer">Bibliothèque</a></li>
<li><a href="#musique" @click="scrollToMusic" class="hover:text-white cursor-pointer">Musique</a></li>
<li><a href="#generator" @click="scrollToGenerator" class="hover:text-white cursor-pointer">Générateur</a></li>
<li><a href="#abonnements" @click="scrollToSubscriptions" class="hover:text-white cursor-pointer">Abonnements</a></li>
</ul>
</div>
<div>
<h5 class="font-semibold mb-4">Support</h5>
<ul class="space-y-2 text-gray-400">
<li><a href="#" class="hover:text-white cursor-pointer">Centre d'aide</a></li>
<li><a href="#" class="hover:text-white cursor-pointer">Contact</a></li>
<li><a href="https://readdy.ai/home/330a5c79-f713-428c-a767-88e47df6061a/1a16829a-79f1-4b29-8fc5-e6e6bf0300cf" data-readdy="true" class="hover:text-white cursor-pointer">Conditions d'utilisation</a></li>
<li><a href="#" class="hover:text-white cursor-pointer">Politique de confidentialité</a></li>
<li><a href="https://readdy.ai/home/330a5c79-f713-428c-a767-88e47df6061a/11cd112c-dbd7-47bf-a3ce-56ae057d705a" data-readdy="true" class="hover:text-white cursor-pointer">Éclaireur</a></li>
</ul>
</div>
<div>
<h5 class="font-semibold mb-4">Suivez-nous</h5>
<div class="flex space-x-4">
<a href="#" class="text-gray-400 hover:text-white cursor-pointer">
<i class="fab fa-facebook text-xl"></i>
</a>
<a href="#" class="text-gray-400 hover:text-white cursor-pointer">
<i class="fab fa-twitter text-xl"></i>
</a>
<a href="#" class="text-gray-400 hover:text-white cursor-pointer">
<i class="fab fa-instagram text-xl"></i>
</a>
<a href="#" class="text-gray-400 hover:text-white cursor-pointer">
<i class="fab fa-youtube text-xl"></i>
</a>
<a href="#" class="text-gray-400 hover:text-white cursor-pointer">
<i class="fab fa-tiktok text-xl"></i>
</a>
</div>
</div>
</div>
<div class="border-t border-gray-800 mt-8 pt-8 text-center text-gray-400">
<p>&copy; 2025 Dossou. Tous droits réservés.</p>
</div>
</div>
</footer>
<!-- Video Modal -->
<div v-if="showVideoModal" class="fixed inset-0 bg-black bg-opacity-90 flex items-center justify-center z-50">
<div class="relative w-full h-full max-w-6xl mx-4 flex flex-col">
<div class="flex items-center justify-between p-4 text-white">
<h3 class="text-2xl font-bold">{{ currentVideo?.title }}</h3>
<button @click="closeVideoModal" class="text-white hover:text-gray-300 text-2xl">
<i class="fas fa-times"></i>
</button>
</div>
<div class="flex-1 flex items-center justify-center">
<div class="relative w-full h-full max-h-[70vh] bg-black rounded-lg overflow-hidden">
<video
ref="videoPlayer"
class="w-full h-full object-contain"
controls
autoplay
>
<source :src="currentVideo?.videoUrl" type="video/mp4">
Votre navigateur ne supporte pas la lecture vidéo.
</video>
</div>
</div>
<div class="p-4 text-white">
<div class="flex items-center justify-between mb-4">
<div>
<h4 class="text-lg font-semibold mb-1">{{ currentVideo?.title }}</h4>
<p class="text-gray-300 text-sm">{{ currentVideo?.description }}</p>
</div>
<div class="text-right text-sm text-gray-300">
<div class="flex items-center space-x-4">
<span><i class="fas fa-eye mr-1"></i>{{ currentVideo?.views || '0' }} vues</span>
<span><i class="fas fa-share mr-1"></i>{{ currentVideo?.shares }} partages</span>
</div>
</div>
</div>
<div class="flex items-center justify-between">
<div class="flex space-x-3">
<button @click="shareToSocial('tiktok')" class="bg-pink-500 text-white px-4 py-2 rounded !rounded-button hover:bg-pink-600 transition-colors cursor-pointer whitespace-nowrap">
<i class="fab fa-tiktok mr-2"></i>Partager sur TikTok
</button>
<button @click="shareToSocial('instagram')" class="bg-gradient-to-r from-purple-500 to-pink-500 text-white px-4 py-2 rounded !rounded-button hover:from-purple-600 hover:to-pink-600 transition-colors cursor-pointer whitespace-nowrap">
<i class="fab fa-instagram mr-2"></i>Instagram
</button>
<button @click="shareToSocial('facebook')" class="bg-blue-600 text-white px-4 py-2 rounded !rounded-button hover:bg-blue-700 transition-colors cursor-pointer whitespace-nowrap">
<i class="fab fa-facebook mr-2"></i>Facebook
</button>
<button @click="shareToSocial('youtube')" class="bg-red-600 text-white px-4 py-2 rounded !rounded-button hover:bg-red-700 transition-colors cursor-pointer whitespace-nowrap">
<i class="fab fa-youtube mr-2"></i>YouTube
</button>
</div>
<button @click="downloadVideo" class="bg-amber-600 text-white px-4 py-2 rounded !rounded-button hover:bg-amber-700 transition-colors cursor-pointer whitespace-nowrap">
<i class="fas fa-download mr-2"></i>Télécharger
</button>
</div>
</div>
</div>
</div>
<!-- Progress Modal -->
<div v-if="showProgressModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
<div class="bg-white rounded-xl shadow-2xl p-8 w-full max-w-lg mx-4">
<div class="text-center">
<div v-if="!generationComplete">
<div class="w-16 h-16 mx-auto mb-6">
<div class="animate-spin rounded-full h-16 w-16 border-b-2 border-amber-600"></div>
</div>
<h3 class="text-2xl font-bold text-gray-800 mb-6">Génération en cours...</h3>
<div class="space-y-4">
<div v-for="(step, index) in generationSteps" :key="index" class="flex items-center space-x-3">
<div class="w-8 h-8 rounded-full flex items-center justify-center"
:class="getStepStatus(index)">
<i v-if="currentStep > index" class="fas fa-check text-white"></i>
<i v-else-if="currentStep === index" class="fas fa-spinner fa-spin text-white"></i>
<span v-else class="text-gray-400 text-sm font-semibold">{{ index + 1 }}</span>
</div>
<div class="text-left">
<p class="font-medium text-gray-800">{{ step.title }}</p>
<p class="text-sm text-gray-500">{{ step.description }}</p>
</div>
</div>
</div>
<div class="mt-6">
<div class="bg-gray-200 rounded-full h-2">
<div class="bg-amber-600 h-2 rounded-full transition-all duration-500"
:style="{ width: progressPercentage + '%' }"></div>
</div>
<p class="text-sm text-gray-600 mt-2">{{ progressPercentage }}% terminé</p>
</div>
</div>
<div v-else>
<div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
<i class="fas fa-check text-green-600 text-2xl"></i>
</div>
<h3 class="text-2xl font-bold text-gray-800 mb-4">Vidéo générée avec succès !</h3>
<p class="text-gray-600 mb-4">
Votre vidéo 4K avec filigrane Dossou a été générée et partagée sur les plateformes sélectionnées.
</p>
<div class="bg-blue-50 border border-blue-200 rounded-lg p-4 mb-6">
<div class="flex items-center space-x-2 text-blue-800">
<i class="fas fa-info-circle"></i>
<p class="font-medium">Crédits restants: {{ userCredits }}</p>
</div>
<p class="text-blue-700 text-sm mt-1">
{{ userCredits === 0 ? 'Souscrivez à un abonnement pour des vidéos illimitées sans filigrane' : 'Vous pouvez créer encore ' + userCredits + ' vidéo(s) gratuite(s)' }}
</p>
</div>
<div class="space-y-3 mb-6">
<div v-for="platform in selectedPlatforms" :key="platform" class="bg-gray-50 rounded-lg p-3 flex items-center justify-between">
<div class="flex items-center space-x-3">
<i :class="getSocialIcon(platform)" :style="{ color: getSocialColor(platform) }" class="text-xl"></i>
<span class="font-medium">{{ platform }}</span>
</div>
<div class="flex items-center space-x-2">
<span class="text-green-600 text-sm"><i class="fas fa-check mr-1"></i>Publié</span>
<button class="text-amber-600 hover:text-amber-700 text-sm font-medium cursor-pointer">
Voir le post
</button>
</div>
</div>
</div>
<div class="flex space-x-3">
<button @click="closeProgressModal" class="flex-1 bg-gray-200 text-gray-800 py-3 !rounded-button hover:bg-gray-300 transition-colors whitespace-nowrap cursor-pointer">
Fermer
</button>
<button @click="generateAnother" class="flex-1 bg-amber-600 text-white py-3 !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer">
Générer une autre
</button>
</div>
</div>
</div>
</div>
</div>
<!-- Subscription Modal -->
<div v-if="showSubscriptionModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
<div class="bg-white rounded-xl shadow-2xl p-8 w-full max-w-2xl mx-4 max-h-[90vh] overflow-y-auto">
<div class="flex items-center justify-between mb-6">
<h3 class="text-2xl font-bold text-gray-800">Finaliser votre abonnement</h3>
<button @click="closeSubscriptionModal" class="text-gray-500 hover:text-gray-700">
<i class="fas fa-times text-xl"></i>
</button>
</div>
<!-- Plan Selected Summary -->
<div class="bg-gradient-to-r from-amber-50 to-orange-50 rounded-lg p-6 mb-6 border-2 border-amber-200">
<div class="flex items-center justify-between">
<div>
<h4 class="text-xl font-bold text-amber-800">{{ selectedPlan?.title }}</h4>
<p class="text-gray-600">{{ selectedPlan?.description }}</p>
</div>
<div class="text-right">
<div class="text-3xl font-bold text-amber-600">{{ selectedPlan?.price }}</div>
<div class="text-sm text-gray-500">{{ selectedPlan?.period }}</div>
</div>
</div>
<div class="mt-4 grid grid-cols-2 gap-3 text-sm">
<div v-for="feature in selectedPlan?.features" :key="feature" class="flex items-center">
<i class="fas fa-check text-green-500 mr-2"></i>
<span>{{ feature }}</span>
</div>
</div>
</div>
<form @submit.prevent="submitSubscription" v-if="!subscriptionSuccess">
<!-- Personal Information -->
<div class="mb-6">
<h5 class="text-lg font-semibold text-gray-800 mb-4">Informations personnelles</h5>
<div class="grid md:grid-cols-2 gap-4">
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">Nom</label>
<input
v-model="subscriptionInfo.lastName"
type="text"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="Votre nom de famille"
>
</div>
<div>
<label class="block text-sm font-medium text-gray-700 mb-2">Prénoms</label>
<input
v-model="subscriptionInfo.firstName"
type="text"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="Vos prénoms"
>
</div>
</div>
<div class="mt-4">
<label class="block text-sm font-medium text-gray-700 mb-2">Email</label>
<input
v-model="subscriptionInfo.email"
type="email"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="votre@email.com"
>
</div>
<div class="mt-4">
<label class="block text-sm font-medium text-gray-700 mb-2">Numéro de téléphone</label>
<input
v-model="subscriptionInfo.phone"
type="tel"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="+229 XX XX XX XX"
>
</div>
</div>
<!-- Payment Method Selection -->
<div class="mb-6">
<h5 class="text-lg font-semibold text-gray-800 mb-4">Méthode de paiement</h5>
<div class="grid md:grid-cols-2 gap-4">
<div v-for="payment in paymentMethods" :key="payment.name"
@click="subscriptionInfo.paymentMethod = payment.name"
class="p-4 border-2 rounded-lg cursor-pointer hover:bg-gray-50 transition-colors"
:class="{ 'border-amber-500 bg-amber-50': subscriptionInfo.paymentMethod === payment.name, 'border-gray-200': subscriptionInfo.paymentMethod !== payment.name }">
<div class="flex items-center space-x-3">
<div class="w-12 h-12 flex items-center justify-center">
<i :class="payment.icon" class="text-2xl" :style="{ color: payment.color }"></i>
</div>
<div>
<h6 class="font-semibold text-gray-800">{{ payment.name }}</h6>
<p class="text-sm text-gray-600">{{ payment.description }}</p>
</div>
</div>
<div class="mt-2 flex items-center">
<input
type="radio"
:value="payment.name"
v-model="subscriptionInfo.paymentMethod"
class="text-amber-600 focus:ring-amber-500"
>
<span class="ml-2 text-sm">Sélectionner</span>
</div>
</div>
</div>
</div>
<!-- Payment Instructions -->
<div v-if="subscriptionInfo.paymentMethod" class="mb-6 bg-blue-50 rounded-lg p-4 border border-blue-200">
<h6 class="font-semibold text-blue-800 mb-2">
<i class="fas fa-info-circle mr-2"></i>
Instructions de paiement - {{ subscriptionInfo.paymentMethod }}
</h6>
<div v-if="subscriptionInfo.paymentMethod === 'MTN Mobile Money'" class="text-sm text-blue-700">
<p class="mb-2">1. Composez *133# sur votre téléphone</p>
<p class="mb-2">2. Sélectionnez "Transfert d'argent"</p>
<p class="mb-2">3. Envoyez <strong>{{ selectedPlan?.priceNumber }} €</strong> au numéro: <strong>+229 01 97 56 31 97</strong></p>
<p>4. Saisissez le code de confirmation reçu ci-dessous</p>
</div>
<div v-if="subscriptionInfo.paymentMethod === 'Moov Money'" class="text-sm text-blue-700">
<p class="mb-2">1. Composez *555# sur votre téléphone</p>
<p class="mb-2">2. Sélectionnez "Envoi d'argent"</p>
<p class="mb-2">3. Envoyez <strong>{{ selectedPlan?.priceNumber }} €</strong> au numéro: <strong>+229 64 64 69 96</strong></p>
<p>4. Saisissez le code de confirmation reçu ci-dessous</p>
</div>
</div>
<!-- Transaction Confirmation -->
<div v-if="subscriptionInfo.paymentMethod && (subscriptionInfo.paymentMethod === 'MTN Mobile Money' || subscriptionInfo.paymentMethod === 'Moov Money')" class="mb-6">
<label class="block text-sm font-medium text-gray-700 mb-2">Code de confirmation de transaction</label>
<input
v-model="subscriptionInfo.transactionCode"
type="text"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="Entrez le code de confirmation reçu par SMS"
>
</div>
<!-- Terms and Conditions -->
<div class="mb-6">
<label class="flex items-start space-x-3 cursor-pointer">
<input
type="checkbox"
v-model="subscriptionInfo.acceptTerms"
required
class="rounded text-amber-600 focus:ring-amber-500 mt-1"
>
<span class="text-sm text-gray-700">
J'accepte les <a href="#" class="text-amber-600 hover:text-amber-700 font-medium">conditions d'utilisation</a>
et la <a href="#" class="text-amber-600 hover:text-amber-700 font-medium">politique de confidentialité</a>
</span>
</label>
</div>
<!-- Submit Button -->
<div class="flex space-x-4">
<button
type="button"
@click="closeSubscriptionModal"
class="flex-1 bg-gray-200 text-gray-800 py-3 !rounded-button hover:bg-gray-300 transition-colors whitespace-nowrap cursor-pointer"
>
Annuler
</button>
<button
type="submit"
class="flex-1 bg-amber-600 text-white py-3 font-semibold !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer"
:disabled="!subscriptionInfo.paymentMethod || !subscriptionInfo.acceptTerms"
:class="{ 'opacity-50 cursor-not-allowed': !subscriptionInfo.paymentMethod || !subscriptionInfo.acceptTerms }"
>
<i class="fas fa-credit-card mr-2"></i>
Confirmer l'abonnement
</button>
</div>
</form>
<!-- Success Message -->
<div v-if="subscriptionSuccess" class="text-center">
<div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
<i class="fas fa-check text-green-600 text-2xl"></i>
</div>
<h4 class="text-xl font-bold text-gray-800 mb-2">Abonnement confirmé !</h4>
<p class="text-gray-600 mb-6">
Merci {{ subscriptionInfo.firstName }} {{ subscriptionInfo.lastName }} !<br>
Votre abonnement <strong>{{ selectedPlan?.title }}</strong> est maintenant actif.<br>
Un email de confirmation a été envoyé à {{ subscriptionInfo.email }}
</p>
<button
@click="closeSubscriptionModal"
class="bg-amber-600 text-white px-6 py-3 !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer"
>
Commencer à utiliser Dossou
</button>
</div>
</div>
</div>
<!-- Share Success Toast -->
<div v-if="showShareToast" class="fixed top-4 right-4 bg-green-500 text-white px-6 py-4 rounded-lg shadow-lg z-50 max-w-sm">
<div class="flex items-center space-x-3">
<i class="fas fa-check-circle text-xl"></i>
<div>
<p class="font-semibold">Partage réussi !</p>
<p class="text-sm text-green-100">{{ shareToastMessage }}</p>
</div>
<button @click="showShareToast = false" class="text-white hover:text-green-200 ml-2">
<i class="fas fa-times"></i>
</button>
</div>
</div>
<!-- Login Modal -->
<div v-if="showLoginModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
<div class="bg-white rounded-xl shadow-2xl p-8 w-full max-w-md mx-4">
<div class="flex items-center justify-between mb-6">
<h3 class="text-2xl font-bold text-gray-800">Se connecter</h3>
<button @click="closeLoginModal" class="text-gray-500 hover:text-gray-700">
<i class="fas fa-times text-xl"></i>
</button>
</div>
<div v-if="!showLoginConfirmation">
<form @submit.prevent="submitLogin">
<div class="mb-4">
<label class="block text-sm font-medium text-gray-700 mb-2">Email</label>
<input
v-model="loginInfo.email"
type="email"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="votre@email.com"
>
</div>
<div class="mb-4">
<label class="block text-sm font-medium text-gray-700 mb-2">Mot de passe</label>
<input
v-model="loginInfo.password"
type="password"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="••••••••"
>
</div>
<div class="flex items-center justify-between mb-6">
<label class="flex items-center">
<input
type="checkbox"
v-model="loginInfo.rememberMe"
class="rounded text-amber-600 focus:ring-amber-500"
>
<span class="ml-2 text-sm text-gray-600">Se souvenir de moi</span>
</label>
<button
type="button"
@click="showForgotPassword = true"
class="text-amber-600 hover:text-amber-700 text-sm font-medium cursor-pointer"
>
Mot de passe oublié ?
</button>
</div>
<button
type="submit"
class="w-full bg-amber-600 text-white py-3 font-semibold !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer mb-4"
>
<i class="fas fa-sign-in-alt mr-2"></i>
Se connecter
</button>
<div class="text-center">
<p class="text-gray-600 text-sm">
Nouveau sur Dossou ?
<button
type="button"
@click="switchToSignup"
class="text-amber-600 hover:text-amber-700 font-medium cursor-pointer ml-1"
>
Créer un compte
</button>
</p>
</div>
</form>
</div>
<div v-else-if="showForgotPassword">
<form @submit.prevent="submitForgotPassword">
<div class="text-center mb-6">
<h4 class="text-xl font-bold text-gray-800 mb-2">Mot de passe oublié ?</h4>
<p class="text-gray-600 text-sm">
Entrez votre adresse email et nous vous enverrons un lien pour réinitialiser votre mot de passe.
</p>
</div>
<div class="mb-6">
<label class="block text-sm font-medium text-gray-700 mb-2">Email</label>
<input
v-model="forgotPasswordEmail"
type="email"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="votre@email.com"
>
</div>
<div class="flex space-x-3">
<button
type="button"
@click="showForgotPassword = false"
class="flex-1 bg-gray-200 text-gray-800 py-3 !rounded-button hover:bg-gray-300 transition-colors whitespace-nowrap cursor-pointer"
>
Retour
</button>
<button
type="submit"
class="flex-1 bg-amber-600 text-white py-3 font-semibold !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer"
>
Envoyer le lien
</button>
</div>
</form>
</div>
<div v-else class="text-center">
<div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
<i class="fas fa-check text-green-600 text-2xl"></i>
</div>
<h4 class="text-xl font-bold text-gray-800 mb-2">Connexion réussie !</h4>
<p class="text-gray-600 mb-6">
Bienvenue {{ loginInfo.firstName || 'back' }} !<br>
Vous êtes maintenant connecté à Dossou.
</p>
<button
@click="closeLoginModal"
class="bg-amber-600 text-white px-6 py-2 !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer"
>
Continuer
</button>
</div>
</div>
</div>
<!-- Account Modal -->
<div v-if="showAccountModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
<div class="bg-white rounded-xl shadow-2xl p-8 w-full max-w-md mx-4">
<div class="flex items-center justify-between mb-6">
<h3 class="text-2xl font-bold text-gray-800">Créer un compte</h3>
<button @click="closeAccountModal" class="text-gray-500 hover:text-gray-700">
<i class="fas fa-times text-xl"></i>
</button>
</div>
<div v-if="!showConfirmation">
<form @submit.prevent="submitAccountInfo">
<div class="mb-4">
<label class="block text-sm font-medium text-gray-700 mb-2">Nom</label>
<input
v-model="accountInfo.lastName"
type="text"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="Votre nom de famille"
>
</div>
<div class="mb-4">
<label class="block text-sm font-medium text-gray-700 mb-2">Prénoms</label>
<input
v-model="accountInfo.firstName"
type="text"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="Vos prénoms"
>
</div>
<div class="mb-4">
<label class="block text-sm font-medium text-gray-700 mb-2">Email</label>
<input
v-model="accountInfo.email"
type="email"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="votre@email.com"
>
</div>
<div class="mb-6">
<label class="block text-sm font-medium text-gray-700 mb-2">Mot de passe</label>
<input
v-model="accountInfo.password"
type="password"
required
class="w-full p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-amber-500 focus:border-transparent"
placeholder="••••••••"
>
</div>
<button
type="submit"
class="w-full bg-amber-600 text-white py-3 font-semibold !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer mb-4"
>
<i class="fas fa-user-plus mr-2"></i>
Créer mon compte
</button>
<div class="text-center">
<p class="text-gray-600 text-sm">
Déjà un compte ?
<button
type="button"
@click="switchToLogin"
class="text-amber-600 hover:text-amber-700 font-medium cursor-pointer ml-1"
>
Se connecter
</button>
</p>
</div>
</form>
</div>
<div v-else class="text-center">
<div class="w-16 h-16 bg-green-100 rounded-full flex items-center justify-center mx-auto mb-4">
<i class="fas fa-check text-green-600 text-2xl"></i>
</div>
<h4 class="text-xl font-bold text-gray-800 mb-2">Inscription Confirmée !</h4>
<p class="text-gray-600 mb-6">
Bienvenue {{ accountInfo.firstName }} {{ accountInfo.lastName }} !<br>
Un email de confirmation a été envoyé à {{ accountInfo.email }}
</p>
<button
@click="closeAccountModal"
class="bg-amber-600 text-white px-6 py-2 !rounded-button hover:bg-amber-700 transition-colors whitespace-nowrap cursor-pointer"
>
Continuer
</button>
</div>
</div>
</div>
</div>
</template>
<script lang="ts" setup>
import { ref } from 'vue';
const promptText = ref('');
const showAccountModal = ref(false);
const showConfirmation = ref(false);
const showLoginModal = ref(false);
const showLoginConfirmation = ref(false);
const showForgotPassword = ref(false);
const forgotPasswordEmail = ref('');
const showVideoModal = ref(false);
const currentVideo = ref(null);
const videoPlayer = ref(null);
const showProgressModal = ref(false);
const generationComplete = ref(false);
const currentStep = ref(0);
const progressPercentage = ref(0);
const showSubscriptionModal = ref(false);
const subscriptionSuccess = ref(false);
const selectedPlan = ref(null);
const accountInfo = ref({
firstName: '',
lastName: '',
email: '',
password: ''
});
const loginInfo = ref({
email: '',
password: '',
rememberMe: false,
firstName: ''
});
const isLoggedIn = ref(false);
const userCredits = ref(0);
const subscriptionInfo = ref({
firstName: '',
lastName: '',
email: '',
phone: '',
paymentMethod: '',
transactionCode: '',
acceptTerms: false
});
const subscriptionPlans = ref({
monthly: {
title: 'Abonnement Mensuel',
description: 'Plan mensuel avec toutes les fonctionnalités',
price: '15 000 FCFA',
priceNumber: '15000',
period: '/mois',
features: [
'Génération illimitée de vidéos',
'Qualité 4K Ultra HD',
'Prompts personnalisés',
'Partage automatique sur réseaux sociaux',
'Support prioritaire'
]
},
yearly: {
title: 'Abonnement Annuel',
description: 'Plan annuel avec 20% d\'économie',
price: '144 000 FCFA',
priceNumber: '144000',
period: '/an',
features: [
'Génération illimitée de vidéos',
'Qualité 4K Ultra HD',
'Prompts personnalisés',
'Partage automatique sur réseaux sociaux',
'Support prioritaire',
'Accès anticipé aux nouvelles fonctionnalités',
'Analytics avancées des réseaux sociaux'
]
}
});
const selectedStyle = ref('4k');
const selectedFormat = ref('vertical');
const selectedDuration = ref('15s');
const selectedPlatforms = ref(['TikTok']);
const generationSteps = ref([
{
title: 'Analyse du prompt',
description: 'Analyse et optimisation de votre demande'
},
{
title: 'Génération de la vidéo 4K',
description: 'Création de votre vidéo avec filigrane Dossou'
},
{
title: 'Optimisation pour les réseaux sociaux',
description: 'Adaptation aux formats des plateformes'
},
{
title: 'Partage en cours',
description: 'Publication sur les réseaux sélectionnés'
}
]);
const videos = ref([
{
id: 1,
title: 'L\'Empire du Mali',
description: 'La grandeur de Mansa Moussa et son pèlerinage légendaire qui a marqué l\'histoire',
duration: '12:45',
shares: '2.3k',
views: '145k',
videoUrl: 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4',
thumbnail: 'https://readdy.ai/api/search-image?query=magnificent%20mali%20empire%20with%20golden%20palace%20and%20mansa%20musa%20in%20traditional%20royal%20attire%20with%20golden%20crown%20against%20warm%20african%20sunset%20background&width=300&height=200&seq=video001&orientation=landscape'
},
{
id: 2,
title: 'Royaume du Kongo',
description: 'Les traditions ancestrales et l\'art royal du royaume du Kongo',
duration: '8:30',
shares: '1.8k',
views: '98k',
videoUrl: 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4',
thumbnail: 'https://readdy.ai/api/search-image?query=ancient%20kongo%20kingdom%20with%20traditional%20african%20architecture%20and%20royal%20ceremonies%20in%20beautiful%20african%20landscape%20with%20golden%20lighting&width=300&height=200&seq=video002&orientation=landscape'
},
{
id: 3,
title: 'Civilisation Nubienne',
description: 'Les pharaons noirs et leur héritage sur les rives du Nil',
duration: '15:20',
shares: '3.1k',
views: '203k',
videoUrl: 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4',
thumbnail: 'https://readdy.ai/api/search-image?query=nubian%20civilization%20with%20black%20pharaohs%20and%20ancient%20pyramids%20along%20the%20nile%20river%20with%20golden%20desert%20background%20and%20royal%20regalia&width=300&height=200&seq=video003&orientation=landscape'
},
{
id: 4,
title: 'Empire Songhaï',
description: 'Tombouctou et ses savants, centre intellectuel de l\'Afrique médiévale',
duration: '10:15',
shares: '2.7k',
views: '134k',
videoUrl: 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerEscapes.mp4',
thumbnail: 'https://readdy.ai/api/search-image?query=songhai%20empire%20with%20timbuktu%20ancient%20libraries%20and%20african%20scholars%20studying%20manuscripts%20in%20traditional%20setting%20with%20warm%20golden%20atmosphere&width=300&height=200&seq=video004&orientation=landscape'
}
]);
const promptLibrary = ref([
{
id: 1,
category: 'Empires',
title: 'L\'Empire du Mali et Mansa Moussa',
prompt: 'Créez une vidéo captivante sur Mansa Moussa, l\'homme le plus riche de l\'histoire, montrant sa richesse légendaire, son pèlerinage à La Mecque et l\'âge d\'or de l\'Empire du Mali au 14ème siècle avec ses mines d\'or et ses routes commerciales',
icon: 'fas fa-crown',
difficulty: 'Facile',
bestPlatforms: ['TikTok', 'Instagram'],
views: '145k',
likes: '12.3k',
shares: '2.1k',
duration: '30s'
},
{
id: 2,
category: 'Royaumes',
title: 'La Reine Nzinga et sa Résistance',
prompt: 'Racontez l\'histoire épique de la Reine Nzinga d\'Angola, guerrière légendaire qui a résisté à la colonisation portugaise pendant 30 ans, ses tactiques militaires innovantes et son leadership exceptionnel au 17ème siècle',
icon: 'fas fa-shield-alt',
difficulty: 'Intermédiaire',
bestPlatforms: ['YouTube', 'Facebook'],
views: '98k',
likes: '8.7k',
shares: '1.5k',
duration: '60s'
},
{
id: 3,
category: 'Civilisations',
title: 'Les Pharaons Noirs de Nubie',
prompt: 'Découvrez la fascinante civilisation nubienne et ses pharaons noirs qui ont conquis et gouverné l\'Égypte pendant près d\'un siècle, leurs pyramides majestueuses à Méroé et leur héritage culturel unique',
icon: 'fas fa-monument',
difficulty: 'Avancé',
bestPlatforms: ['YouTube', 'Instagram'],
views: '203k',
likes: '18.9k',
shares: '3.2k',
duration: '3min'
},
{
id: 4,
category: 'Commerce',
title: 'Les Routes de l\'Or au Ghana Antique',
prompt: 'Explorez l\'Empire du Ghana, premier grand empire ouest-africain, ses routes commerciales de l\'or et du sel, la prospérité de ses marchés et l\'influence de Koumbi Saleh capitale commerciale',
icon: 'fas fa-coins',
difficulty: 'Facile',
bestPlatforms: ['TikTok', 'Facebook'],
views: '87k',
likes: '7.2k',
shares: '1.3k',
duration: '15s'
},
{
id: 5,
category: 'Culture',
title: 'Les Bronzes du Bénin',
prompt: 'Plongez dans l\'art raffiné du Royaume du Bénin avec ses célèbres bronzes, témoins d\'une civilisation sophistiquée, leur technique de fonte à la cire perdue et leur signification culturelle profonde',
icon: 'fas fa-palette',
difficulty: 'Intermédiaire',
bestPlatforms: ['Instagram', 'YouTube'],
views: '76k',
likes: '6.8k',
shares: '1.1k',
duration: '45s'
},
{
id: 6,
category: 'Sciences',
title: 'Tombouctou, Université du Désert',
prompt: 'Découvrez Tombouctou au temps de l\'Empire Songhaï, centre intellectuel mondial avec ses universités, ses manuscrits précieux, ses savants réputés et son rayonnement académique à travers l\'Afrique et le monde arabe',
icon: 'fas fa-book',
difficulty: 'Avancé',
bestPlatforms: ['YouTube', 'Facebook'],
views: '134k',
likes: '11.7k',
shares: '2.8k',
duration: '90s'
}
]);
const socialPlatforms = ref([
{
name: 'TikTok',
icon: 'fab fa-tiktok',
color: '#000000'
},
{
name: 'Instagram',
icon: 'fab fa-instagram',
color: '#E4405F'
},
{
name: 'Facebook',
icon: 'fab fa-facebook',
color: '#1877F2'
},
{
name: 'YouTube',
icon: 'fab fa-youtube',
color: '#FF0000'
}
]);
const paymentMethods = ref([
{
name: 'MTN Mobile Money',
description: 'Dépôt: +229 01 97 56 31 97',
icon: 'fas fa-mobile-alt',
color: '#FFD700'
},
{
name: 'Moov Money',
description: 'Dépôt: +229 64 64 69 96',
icon: 'fas fa-credit-card',
color: '#FF6B35'
},
{
name: 'Carte Visa',
description: 'Paiement par carte bancaire',
icon: 'fab fa-cc-visa',
color: '#1A1F71'
},
{
name: 'Wave',
description: 'Transfert instantané',
icon: 'fas fa-wave-square',
color: '#4285F4'
}
]);
const testimonials = ref([
{
id: 1,
name: 'Aminata Traoré',
role: 'Professeure d\'Histoire',
comment: 'Dossou révolutionne l\'enseignement de l\'histoire africaine. Les vidéos 4K sont d\'une qualité exceptionnelle et le partage automatique sur les réseaux sociaux facilite la diffusion du savoir.',
avatar: 'https://readdy.ai/api/search-image?query=professional%20african%20woman%20teacher%20smiling%20warmly%20in%20modern%20classroom%20setting%20with%20books%20and%20african%20cultural%20elements%20in%20background&width=100&height=100&seq=avatar001&orientation=squarish'
},
{
id: 2,
name: 'Kofi Asante',
role: 'Créateur de contenu TikTok',
comment: 'Grâce à Dossou, mes vidéos sur l\'histoire africaine génèrent des millions de vues. La bibliothèque de prompts est une mine d\'or pour créer du contenu viral.',
avatar: 'https://readdy.ai/api/search-image?query=young%20african%20male%20content%20creator%20with%20modern%20studio%20setup%20smiling%20confidently%20with%20camera%20equipment%20and%20social%20media%20graphics%20in%20background&width=100&height=100&seq=avatar002&orientation=squarish'
},
{
id: 3,
name: 'Fatou Diallo',
role: 'Influenceuse Instagram',
comment: 'La plateforme Dossou m\'a permis de faire connaître l\'histoire africaine à ma communauté de 500k followers. Le partage automatique est un gain de temps énorme.',
avatar: 'https://readdy.ai/api/search-image?query=stylish%20african%20woman%20influencer%20taking%20selfie%20with%20ring%20light%20and%20social%20media%20content%20creation%20setup%20with%20african%20cultural%20decorations&width=100&height=100&seq=avatar003&orientation=squarish'
}
]);
const usePrompt = (promptExample: any, specificPlatform?: string) => {
// Fill the prompt text
promptText.value = promptExample.prompt;
// Pre-configure settings based on specific platform or prompt characteristics
if (specificPlatform === 'Instagram') {
selectedFormat.value = 'vertical';
selectedDuration.value = '30s';
selectedPlatforms.value = ['Instagram'];
} else if (specificPlatform === 'TikTok') {
selectedFormat.value = 'vertical';
selectedDuration.value = '15s';
selectedPlatforms.value = ['TikTok'];
} else if (specificPlatform === 'YouTube') {
selectedFormat.value = 'horizontal';
selectedDuration.value = '3min';
selectedPlatforms.value = ['YouTube'];
} else if (specificPlatform === 'Facebook') {
selectedFormat.value = 'horizontal';
selectedDuration.value = '60s';
selectedPlatforms.value = ['Facebook'];
} else if (promptExample.bestPlatforms.includes('TikTok')) {
selectedFormat.value = 'vertical';
selectedDuration.value = '15s';
selectedPlatforms.value = [...promptExample.bestPlatforms];
} else if (promptExample.bestPlatforms.includes('Instagram')) {
selectedFormat.value = 'vertical';
selectedDuration.value = '30s';
selectedPlatforms.value = [...promptExample.bestPlatforms];
} else if (promptExample.bestPlatforms.includes('YouTube')) {
selectedFormat.value = 'horizontal';
selectedDuration.value = '3min';
selectedPlatforms.value = [...promptExample.bestPlatforms];
} else {
selectedFormat.value = 'horizontal';
selectedDuration.value = '60s';
selectedPlatforms.value = [...promptExample.bestPlatforms];
}
// Set style based on difficulty
if (promptExample.difficulty === 'Facile') {
selectedStyle.value = '4k';
} else {
selectedStyle.value = 'animation';
}
// Scroll to generator section
setTimeout(() => {
const generatorSection = document.getElementById('generator');
if (generatorSection) {
generatorSection.scrollIntoView({
behavior: 'smooth',
block: 'start'
});
}
}, 100);
};
const generateVideo = () => {
if (!promptText.value.trim() || !isLoggedIn.value || userCredits.value === 0) {
if (!isLoggedIn.value) {
openLoginModal();
return;
}
return;
}
// Deduct one credit
userCredits.value--;
showProgressModal.value = true;
generationComplete.value = false;
currentStep.value = 0;
progressPercentage.value = 0;
// Simulate generation process
const steps = [
{ duration: 2000, progress: 25 }, // Analyse du prompt
{ duration: 4000, progress: 50 }, // Génération de la vidéo 4K avec filigrane
{ duration: 2000, progress: 75 }, // Optimisation pour les réseaux sociaux
{ duration: 2000, progress: 100 } // Partage en cours
];
let totalTime = 0;
steps.forEach((step, index) => {
setTimeout(() => {
currentStep.value = index;
progressPercentage.value = step.progress;
if (index === steps.length - 1) {
setTimeout(() => {
generationComplete.value = true;
}, 1000);
}
}, totalTime);
totalTime += step.duration;
});
console.log('Generating video with:', {
prompt: promptText.value,
style: selectedStyle.value,
format: selectedFormat.value,
duration: selectedDuration.value,
platforms: selectedPlatforms.value
});
};
const openAccountModal = () => {
showAccountModal.value = true;
showConfirmation.value = false;
};
const closeAccountModal = () => {
showAccountModal.value = false;
showConfirmation.value = false;
// Reset form
accountInfo.value = {
firstName: '',
lastName: '',
email: '',
password: ''
};
};
const openVideoModal = (video) => {
currentVideo.value = video;
showVideoModal.value = true;
};
const closeVideoModal = () => {
showVideoModal.value = false;
currentVideo.value = null;
if (videoPlayer.value) {
videoPlayer.value.pause();
}
};
const shareToSocial = (platform) => {
console.log(`Sharing video "${currentVideo.value?.title}" to ${platform}`);
if (platform === 'facebook' && currentVideo.value) {
// Prepare Facebook sharing parameters
const shareUrl = encodeURIComponent(currentVideo.value.videoUrl);
const title = encodeURIComponent(currentVideo.value.title);
const description = encodeURIComponent(currentVideo.value.description);
// Open Facebook sharing window
const facebookUrl = `https://www.facebook.com/sharer/sharer.php?u=${shareUrl}&quote=${title} - ${description}`;
window.open(facebookUrl, 'facebook-share', 'width=600,height=400,scrollbars=yes,resizable=yes');
// Show success toast
showShareToast.value = true;
shareToastMessage.value = `Vidéo "${currentVideo.value.title}" partagée sur Facebook avec succès !`;
setTimeout(() => {
showShareToast.value = false;
}, 3000);
}
// Ici on ajouterait la logique de partage spécifique à chaque plateforme
};
const downloadVideo = () => {
if (currentVideo.value?.videoUrl) {
const link = document.createElement('a');
link.href = currentVideo.value.videoUrl;
link.download = `${currentVideo.value.title}.mp4`;
document.body.appendChild(link);
link.click();
document.body.removeChild(link);
}
};
const submitAccountInfo = () => {
if (accountInfo.value.firstName && accountInfo.value.lastName && accountInfo.value.email) {
// After account creation, log them in with credits
isLoggedIn.value = true;
userCredits.value = 2; // Give 2 credits for new account
loginInfo.value.firstName = accountInfo.value.firstName;
showConfirmation.value = true;
console.log('Account created:', accountInfo.value);
}
};
const getStepStatus = (index: number) => {
if (currentStep.value > index) {
return 'bg-green-500';
} else if (currentStep.value === index) {
return 'bg-amber-600';
} else {
return 'bg-gray-300';
}
};
const getSocialIcon = (platform: string) => {
const icons: { [key: string]: string } = {
'TikTok': 'fab fa-tiktok',
'Instagram': 'fab fa-instagram',
'Facebook': 'fab fa-facebook',
'YouTube': 'fab fa-youtube'
};
return icons[platform] || 'fas fa-share';
};
const getSocialColor = (platform: string) => {
const colors: { [key: string]: string } = {
'TikTok': '#000000',
'Instagram': '#E4405F',
'Facebook': '#1877F2',
'YouTube': '#FF0000'
};
return colors[platform] || '#666666';
};
const showShareToast = ref(false);
const shareToastMessage = ref('');
// Music composition variables
const musicText = ref('');
const selectedMusicStyle = ref('Afrobeat');
const musicTempo = ref('modéré');
const musicDuration = ref('1min');
const musicInstruments = ref('traditionnel');
const generatedMusics = ref([]);
const showMusicModal = ref(false);
const currentMusic = ref(null);
const musicStyles = ref([
{
name: 'Afrobeat',
origin: 'Nigeria',
icon: 'fas fa-drum',
color: '#FF6B35',
description: 'Fusion jazz-funk avec percussions africaines'
},
{
name: 'Makossa',
origin: 'Cameroun',
icon: 'fas fa-guitar',
color: '#4ECDC4',
description: 'Rythme urbain camerounais énergique'
},
{
name: 'Mbalax',
origin: 'Sénégal',
icon: 'fas fa-music',
color: '#45B7D1',
description: 'Musique traditionnelle sénégalaise moderne'
},
{
name: 'Coupé-Décalé',
origin: 'Côte d\'Ivoire',
icon: 'fas fa-compact-disc',
color: '#96CEB4',
description: 'Danse électronique ivoirienne festive'
},
{
name: 'Rumba Congolaise',
origin: 'RD Congo',
icon: 'fas fa-violin',
color: '#FFEAA7',
description: 'Rumba authentique du bassin du Congo'
},
{
name: 'Azonto',
origin: 'Ghana',
icon: 'fas fa-headphones',
color: '#FD79A8',
description: 'Hip-hop ghanéen avec percussions locales'
},
{
name: 'Gqom',
origin: 'Afrique du Sud',
icon: 'fas fa-volume-up',
color: '#A29BFE',
description: 'House music sud-africaine minimaliste'
},
{
name: 'Wassoulou',
origin: 'Mali',
icon: 'fas fa-microphone',
color: '#F39C12',
description: 'Musique traditionnelle malienne authentique'
},
{
name: 'Soul',
origin: 'International',
icon: 'fas fa-heart',
color: '#E17055',
description: 'Soul classique avec influences africaines'
},
{
name: 'Jazz Fusion',
origin: 'International',
icon: 'fas fa-saxophone-alt',
color: '#00B894',
description: 'Jazz moderne avec rythmes africains'
},
{
name: 'Rock Africain',
origin: 'International',
icon: 'fas fa-bolt',
color: '#E84393',
description: 'Rock énergique aux sonorités africaines'
},
{
name: 'Rap Afro',
origin: 'International',
icon: 'fas fa-microphone-alt',
color: '#2D3436',
description: 'Hip-hop avec samples africains traditionnels'
}
]);
const closeProgressModal = () => {
showProgressModal.value = false;
generationComplete.value = false;
currentStep.value = 0;
progressPercentage.value = 0;
};
const generateAnother = () => {
closeProgressModal();
promptText.value = '';
if (userCredits.value === 0) {
// If no more credits, scroll to subscription section
setTimeout(() => {
const subscriptionSection = document.querySelector('.py-16.bg-gradient-to-br.from-amber-50.to-orange-100');
if (subscriptionSection) {
subscriptionSection.scrollIntoView({
behavior: 'smooth',
block: 'start'
});
}
}, 100);
}
};
const logout = () => {
isLoggedIn.value = false;
userCredits.value = 0;
loginInfo.value = {
email: '',
password: '',
rememberMe: false,
firstName: ''
};
};
const openLoginModal = () => {
showLoginModal.value = true;
};
const closeLoginModal = () => {
showLoginModal.value = false;
showLoginConfirmation.value = false;
showForgotPassword.value = false;
// Reset form but keep login state
const currentFirstName = loginInfo.value.firstName;
loginInfo.value = {
email: '',
password: '',
rememberMe: false,
firstName: currentFirstName
};
forgotPasswordEmail.value = '';
};
const submitLogin = () => {
if (loginInfo.value.email && loginInfo.value.password) {
console.log('Login attempt:', loginInfo.value);
// Simulate successful login with credits
isLoggedIn.value = true;
userCredits.value = 2; // Give 2 credits for new login
loginInfo.value.firstName = 'Utilisateur'; // Simulate getting user name
showLoginConfirmation.value = true;
setTimeout(() => {
closeLoginModal();
}, 2000);
}
};
const submitForgotPassword = () => {
if (forgotPasswordEmail.value) {
console.log('Password reset requested for:', forgotPasswordEmail.value);
// Show success message and return to login
showForgotPassword.value = false;
// You could show a toast message here
alert(`Un lien de réinitialisation a été envoyé à ${forgotPasswordEmail.value}`);
}
};
const switchToSignup = () => {
closeLoginModal();
openAccountModal();
};
const switchToLogin = () => {
closeAccountModal();
openLoginModal();
};
const selectSubscriptionPlan = (planType: 'monthly' | 'yearly') => {
selectedPlan.value = subscriptionPlans.value[planType];
showSubscriptionModal.value = true;
subscriptionSuccess.value = false;
};
const closeSubscriptionModal = () => {
showSubscriptionModal.value = false;
subscriptionSuccess.value = false;
selectedPlan.value = null;
// Reset form
subscriptionInfo.value = {
firstName: '',
lastName: '',
email: '',
phone: '',
paymentMethod: '',
transactionCode: '',
acceptTerms: false
};
};
const submitSubscription = () => {
if (subscriptionInfo.value.firstName &&
subscriptionInfo.value.lastName &&
subscriptionInfo.value.email &&
subscriptionInfo.value.phone &&
subscriptionInfo.value.paymentMethod &&
subscriptionInfo.value.acceptTerms) {
// For mobile money, require transaction code
if ((subscriptionInfo.value.paymentMethod === 'MTN Mobile Money' ||
subscriptionInfo.value.paymentMethod === 'Moov Money') &&
!subscriptionInfo.value.transactionCode) {
return;
}
subscriptionSuccess.value = true;
console.log('Subscription created:', {
plan: selectedPlan.value,
userInfo: subscriptionInfo.value
});
}
};
const startJourney = () => {
// Scroll to the video generator section
const generatorSection = document.getElementById('generator');
if (generatorSection) {
generatorSection.scrollIntoView({
behavior: 'smooth',
block: 'start'
});
}
};
const scrollToGenerator = () => {
const generatorSection = document.getElementById('generator');
if (generatorSection) {
generatorSection.scrollIntoView({
behavior: 'smooth',
block: 'start'
});
}
};
const scrollToSubscriptions = () => {
const subscriptionsSection = document.getElementById('abonnements');
if (subscriptionsSection) {
subscriptionsSection.scrollIntoView({
behavior: 'smooth',
block: 'start'
});
}
};
const scrollToTop = () => {
window.scrollTo({
top: 0,
behavior: 'smooth'
});
};
const scrollToMusic = () => {
const musicSection = document.getElementById('musique');
if (musicSection) {
musicSection.scrollIntoView({
behavior: 'smooth',
block: 'start'
});
}
};
const generateMusic = () => {
if (!musicText.value.trim() || !isLoggedIn.value || userCredits.value === 0) {
if (!isLoggedIn.value) {
openLoginModal();
return;
}
return;
}
// Deduct one credit
userCredits.value--;
// Find selected style object
const selectedStyle = musicStyles.value.find(style => style.name === selectedMusicStyle.value);
// Create new music composition
const newMusic = {
id: Date.now(),
title: `Composition ${selectedMusicStyle.value}`,
description: musicText.value.substring(0, 100) + '...',
style: selectedStyle,
tempo: musicTempo.value,
duration: musicDuration.value,
instruments: musicInstruments.value,
audioUrl: 'https://www.soundjay.com/misc/sounds/bell-ringing-05.wav', // Placeholder
originalText: musicText.value
};
// Add to generated musics
generatedMusics.value.unshift(newMusic);
// Clear form
musicText.value = '';
// Show success message
showShareToast.value = true;
shareToastMessage.value = `Composition "${selectedMusicStyle.value}" générée avec succès !`;
setTimeout(() => {
showShareToast.value = false;
}, 3000);
console.log('Generating music with:', {
text: musicText.value,
style: selectedMusicStyle.value,
tempo: musicTempo.value,
duration: musicDuration.value,
instruments: musicInstruments.value
});
};
const playMusic = (music) => {
currentMusic.value = music;
console.log('Playing music:', music.title);
// Here you would implement actual audio playback
showShareToast.value = true;
shareToastMessage.value = `Lecture de "${music.title}" en cours...`;
setTimeout(() => {
showShareToast.value = false;
}, 2000);
};
const downloadMusic = (music) => {
console.log('Downloading music:', music.title);
// Here you would implement actual download functionality
showShareToast.value = true;
shareToastMessage.value = `Téléchargement de "${music.title}" commencé...`;
setTimeout(() => {
showShareToast.value = false;
}, 2000);
};
const shareMusic = (music) => {
console.log('Sharing music:', music.title);
// Here you would implement sharing functionality
showShareToast.value = true;
shareToastMessage.value = `Partage de "${music.title}" sur les réseaux sociaux...`;
setTimeout(() => {
showShareToast.value = false;
}, 3000);
};
</script>
<style scoped>
body {
min-height: 1024px;
}
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
-webkit-appearance: none;
margin: 0;
}
input[type="number"] {
-moz-appearance: textfield;
}
.line-clamp-3 {
display: -webkit-box;
-webkit-line-clamp: 3;
-webkit-box-orient: vertical;
overflow: hidden;
}
</style>