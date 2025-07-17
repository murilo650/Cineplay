<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Painel IPTV Premium</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Custom scrollbar */
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #1e293b;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #64748b;
            border-radius: 3px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
        
        /* Animation for channel change */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .fade-in {
            animation: fadeIn 0.5s ease-in-out;
        }
        
        /* Gradient background */
        .gradient-bg {
            background: linear-gradient(135deg, #1e3a8a 0%, #0f172a 100%);
        }
    </style>
</head>
<body class="gradient-bg min-h-screen text-gray-100">
    <div class="container mx-auto px-4 py-8">
        <!-- Header -->
        <header class="flex flex-col md:flex-row justify-between items-center mb-8">
            <div class="flex items-center mb-4 md:mb-0">
                <i class="fas fa-tv text-blue-400 text-3xl mr-3"></i>
                <h1 class="text-2xl md:text-3xl font-bold bg-gradient-to-r from-blue-400 to-blue-600 bg-clip-text text-transparent">
                    IPTV Premium
                </h1>
            </div>
            
            <div class="flex items-center space-x-4">
                <div class="relative">
                    <input type="text" placeholder="Buscar canal..." 
                           class="bg-slate-800 rounded-full py-2 px-4 pl-10 focus:outline-none focus:ring-2 focus:ring-blue-500 w-48 md:w-64">
                    <i class="fas fa-search absolute left-3 top-3 text-gray-400"></i>
                </div>
                <button class="bg-blue-600 hover:bg-blue-700 rounded-full px-4 py-2 flex items-center">
                    <i class="fas fa-user mr-2"></i>
                    <span class="hidden md:inline">Minha Conta</span>
                </button>
            </div>
        </header>
        
        <div class="flex flex-col lg:flex-row gap-6">
            <!-- Main Player Section -->
            <div class="lg:w-2/3">
                <div class="bg-slate-900 rounded-xl overflow-hidden shadow-2xl mb-6">
                    <div class="aspect-w-16 aspect-h-9 relative">
                        <video id="player" class="w-full h-auto fade-in" poster="https://via.placeholder.com/1280x720/1e293b/64748b?text=IPTV+Premium" controls>
                            <source src="" type="video/mp4">
                            Seu navegador não suporta o elemento de vídeo.
                        </video>
                        <div id="channel-info" class="absolute bottom-0 left-0 right-0 bg-gradient-to-t from-black/80 to-transparent p-4 hidden">
                            <h3 class="font-bold text-xl" id="current-channel-name">Nome do Canal</h3>
                            <p class="text-sm text-gray-300" id="current-channel-description">Descrição do canal atual</p>
                        </div>
                        <button id="info-btn" class="absolute top-4 right-4 bg-black/50 rounded-full p-2 hover:bg-black/70">
                            <i class="fas fa-info-circle text-white"></i>
                        </button>
                    </div>
                </div>
                
                <div class="bg-slate-800/50 rounded-xl p-6 shadow-lg">
                    <h2 class="text-xl font-bold mb-4 flex items-center">
                        <i class="fas fa-list mr-2 text-blue-400"></i>
                        Controles do Player
                    </h2>
                    <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                        <button class="bg-slate-700 hover:bg-slate-600 rounded-lg p-3 flex flex-col items-center">
                            <i class="fas fa-volume-up text-blue-400 mb-1"></i>
                            <span class="text-sm">Volume</span>
                        </button>
                        <button class="bg-slate-700 hover:bg-slate-600 rounded-lg p-3 flex flex-col items-center">
                            <i class="fas fa-closed-captioning text-blue-400 mb-1"></i>
                            <span class="text-sm">Legendas</span>
                        </button>
                        <button class="bg-slate-700 hover:bg-slate-600 rounded-lg p-3 flex flex-col items-center">
                            <i class="fas fa-cog text-blue-400 mb-1"></i>
                            <span class="text-sm">Qualidade</span>
                        </button>
                        <button class="bg-slate-700 hover:bg-slate-600 rounded-lg p-3 flex flex-col items-center">
                            <i class="fas fa-expand text-blue-400 mb-1"></i>
                            <span class="text-sm">Tela Cheia</span>
                        </button>
                    </div>
                </div>
            </div>
            
            <!-- Channels List Section -->
            <div class="lg:w-1/3">
                <div class="bg-slate-800/50 rounded-xl shadow-lg overflow-hidden">
                    <div class="flex border-b border-slate-700">
                        <button class="category-tab active py-3 px-4 font-medium text-blue-400 border-b-2 border-blue-400">
                            <i class="fas fa-bolt mr-2"></i> Todos
                        </button>
                        <button class="category-tab py-3 px-4 font-medium text-gray-400 hover:text-white">
                            <i class="fas fa-futbol mr-2"></i> Esportes
                        </button>
                        <button class="category-tab py-3 px-4 font-medium text-gray-400 hover:text-white">
                            <i class="fas fa-film mr-2"></i> Filmes
                        </button>
                    </div>
                    
                    <div class="h-96 overflow-y-auto custom-scrollbar">
                        <div class="divide-y divide-slate-700">
                            <!-- Channel items will be added here by JavaScript -->
                        </div>
                    </div>
                    
                    <div class="p-4 bg-slate-900/50 flex justify-between items-center">
                        <div class="text-sm text-gray-400">
                            <span id="current-time">00:00</span> | 
                            <span id="total-channels">0</span> Canais
                        </div>
                        <div class="flex space-x-2">
                            <button id="prev-btn" class="p-2 bg-slate-700 rounded-full hover:bg-blue-600 disabled:opacity-50" disabled>
                                <i class="fas fa-chevron-left"></i>
                            </button>
                            <button id="next-btn" class="p-2 bg-slate-700 rounded-full hover:bg-blue-600 disabled:opacity-50" disabled>
                                <i class="fas fa-chevron-right"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Favorites Section -->
        <div class="mt-8 bg-slate-800/50 rounded-xl p-6 shadow-lg">
            <h2 class="text-xl font-bold mb-4 flex items-center">
                <i class="fas fa-star text-yellow-400 mr-2"></i>
                Canais Favoritos
            </h2>
            <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-4" id="favorites-container">
                <!-- Favorite channels will be added here -->
                <div class="text-center text-gray-400 py-8">
                    <i class="fas fa-star text-2xl mb-2"></i>
                    <p>Adicione canais aos favoritos</p>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Sample channel data
            const channels = [
                { id: 1, name: "Globo HD", category: "geral", logo: "https://via.placeholder.com/80/1e293b/64748b?text=GLOBO", url: "https://sample-stream.com/globo.m3u8", isFavorite: true, description: "Canal líder de audiência no Brasil" },
                { id: 2, name: "SporTV HD", category: "esportes", logo: "https://via.placeholder.com/80/1e293b/64748b?text=SPORTV", url: "https://sample-stream.com/sportv.m3u8", isFavorite: false, description: "O melhor do esporte brasileiro e internacional" },
                { id: 3, name: "HBO HD", category: "filmes", logo: "https://via.placeholder.com/80/1e293b/64748b?text=HBO", url: "https://sample-stream.com/hbo.m3u8", isFavorite: true, description: "Os melhores filmes e séries exclusivas" },
                { id: 4, name: "Discovery HD", category: "documentarios", logo: "https://via.placeholder.com/80/1e293b/64748b?text=DISCOVERY", url: "https://sample-stream.com/discovery.m3u8", isFavorite: false, description: "Documentários e programas educativos" },
                { id: 5, name: "Band HD", category: "geral", logo: "https://via.placeholder.com/80/1e293b/64748b?text=BAND", url: "https://sample-stream.com/band.m3u8", isFavorite: false, description: "Jornalismo e variedades" },
                { id: 6, name: "Fox Sports HD", category: "esportes", logo: "https://via.placeholder.com/80/1e293b/64748b?text=FOX+SPORTS", url: "https://sample-stream.com/foxsports.m3u8", isFavorite: true, description: "Transmissões esportivas internacionais" },
                { id: 7, name: "TNT HD", category: "filmes", logo: "https://via.placeholder.com/80/1e293b/64748b?text=TNT", url: "https://sample-stream.com/tnt.m3u8", isFavorite: false, description: "Filmes e séries premiados" },
                { id: 8, name: "National Geographic", category: "documentarios", logo: "https://via.placeholder.com/80/1e293b/64748b?text=NAT+GEO", url: "https://sample-stream.com/natgeo.m3u8", isFavorite: false, description: "Explorando nosso planeta" },
                { id: 9, name: "Record HD", category: "geral", logo: "https://via.placeholder.com/80/1e293b/64748b?text=RECORD", url: "https://sample-stream.com/record.m3u8", isFavorite: false, description: "Programação diversificada" },
                { id: 10, name: "ESPN HD", category: "esportes", logo: "https://via.placeholder.com/80/1e293b/64748b?text=ESPN", url: "https://sample-stream.com/espn.m3u8", isFavorite: true, description: "Esportes americanos e internacionais" }
            ];
            
            // DOM elements
            const player = document.getElementById('player');
            const channelList = document.querySelector('.divide-y');
            const favoritesContainer = document.getElementById('favorites-container');
            const currentChannelName = document.getElementById('current-channel-name');
            const currentChannelDesc = document.getElementById('current-channel-description');
            const channelInfo = document.getElementById('channel-info');
            const infoBtn = document.getElementById('info-btn');
            const prevBtn = document.getElementById('prev-btn');
            const nextBtn = document.getElementById('next-btn');
            const categoryTabs = document.querySelectorAll('.category-tab');
            const totalChannels = document.getElementById('total-channels');
            const currentTime = document.getElementById('current-time');
            
            let currentChannelIndex = 0;
            
            // Update current time
            function updateTime() {
                const now = new Date();
                const hours = now.getHours().toString().padStart(2, '0');
                const minutes = now.getMinutes().toString().padStart(2, '0');
                currentTime.textContent = `${hours}:${minutes}`;
            }
            
            setInterval(updateTime, 1000);
            updateTime();
            
            // Load channels into the list
            function loadChannels(filter = 'all') {
                channelList.innerHTML = '';
                let filteredChannels = channels;
                
                if (filter !== 'all') {
                    filteredChannels = channels.filter(channel => channel.category === filter);
                }
                
                filteredChannels.forEach((channel, index) => {
                    const channelItem = document.createElement('div');
                    channelItem.className = `p-3 hover:bg-slate-700/50 cursor-pointer flex items-center ${index === currentChannelIndex && filteredChannels[currentChannelIndex].id === channel.id ? 'bg-slate-700' : ''}`;
                    channelItem.innerHTML = `
                        <img src="${channel.logo}" alt="${channel.name}" class="w-10 h-10 rounded-md mr-3">
                        <div class="flex-1">
                            <h3 class="font-medium">${channel.name}</h3>
                            <p class="text-xs text-gray-400">${channel.category}</p>
                        </div>
                        <button class="favorite-btn p-2 text-${channel.isFavorite ? 'yellow-400' : 'gray-500'} hover:text-yellow-400" data-id="${channel.id}">
                            <i class="fas fa-star"></i>
                        </button>
                    `;
                    
                    channelItem.addEventListener('click', () => {
                        playChannel(channel, index);
                    });
                    
                    channelList.appendChild(channelItem);
                });
                
                totalChannels.textContent = filteredChannels.length;
                updateNavigationButtons();
            }
            
            // Play selected channel
            function playChannel(channel, index) {
                currentChannelIndex = index;
                player.src = channel.url;
                player.load();
                player.play().catch(e => console.log("Autoplay prevented:", e));
                
                currentChannelName.textContent = channel.name;
                currentChannelDesc.textContent = channel.description;
                
                // Update active channel in list
                document.querySelectorAll('.divide-y > div').forEach((item, i) => {
                    if (i === index) {
                        item.classList.add('bg-slate-700');
                    } else {
                        item.classList.remove('bg-slate-700');
                    }
                });
                
                // Add fade-in effect
                player.classList.add('fade-in');
                setTimeout(() => player.classList.remove('fade-in'), 500);
                
                // Update favorites display
                updateFavorites();
            }
            
            // Update favorites display
            function updateFavorites() {
                const favoriteChannels = channels.filter(channel => channel.isFavorite);
                
                if (favoriteChannels.length > 0) {
                    favoritesContainer.innerHTML = '';
                    
                    favoriteChannels.forEach(channel => {
                        const favItem = document.createElement('div');
                        favItem.className = 'cursor-pointer group';
                        favItem.innerHTML = `
                            <div class="bg-slate-700/50 rounded-lg p-3 group-hover:bg-slate-600 transition-all">
                                <img src="${channel.logo}" alt="${channel.name}" class="w-full h-auto rounded-md mb-2">
                                <h3 class="text-sm font-medium text-center truncate">${channel.name}</h3>
                            </div>
                        `;
                        
                        favItem.addEventListener('click', () => {
                            const channelIndex = channels.findIndex(c => c.id === channel.id);
                            playChannel(channel, channelIndex);
                        });
                        
                        favoritesContainer.appendChild(favItem);
                    });
                }
            }
            
            // Update navigation buttons state
            function updateNavigationButtons() {
                prevBtn.disabled = currentChannelIndex <= 0;
                nextBtn.disabled = currentChannelIndex >= channels.length - 1;
            }
            
            // Event listeners
            infoBtn.addEventListener('click', () => {
                channelInfo.classList.toggle('hidden');
            });
            
            prevBtn.addEventListener('click', () => {
                if (currentChannelIndex > 0) {
                    currentChannelIndex--;
                    playChannel(channels[currentChannelIndex], currentChannelIndex);
                }
            });
            
            nextBtn.addEventListener('click', () => {
                if (currentChannelIndex < channels.length - 1) {
                    currentChannelIndex++;
                    playChannel(channels[currentChannelIndex], currentChannelIndex);
                }
            });
            
            // Category tabs
            categoryTabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    categoryTabs.forEach(t => t.classList.remove('active', 'text-blue-400', 'border-blue-400'));
                    tab.classList.add('active', 'text-blue-400', 'border-blue-400');
                    
                    const category = tab.textContent.trim().toLowerCase();
                    let filter = 'all';
                    
                    if (category.includes('esportes')) filter = 'esportes';
                    else if (category.includes('filmes')) filter = 'filmes';
                    else if (category.includes('documentários')) filter = 'documentarios';
                    
                    loadChannels(filter);
                });
            });
            
            // Favorite button event delegation
            document.addEventListener('click', (e) => {
                if (e.target.classList.contains('favorite-btn') || e.target.closest('.favorite-btn')) {
                    const btn = e.target.classList.contains('favorite-btn') ? e.target : e.target.closest('.favorite-btn');
                    const channelId = parseInt(btn.dataset.id);
                    
                    const channelIndex = channels.findIndex(c => c.id === channelId);
                    if (channelIndex !== -1) {
                        channels[channelIndex].isFavorite = !channels[channelIndex].isFavorite;
                        
                        // Update button color
                        const icon = btn.querySelector('i') || btn;
                        if (channels[channelIndex].isFavorite) {
                            icon.classList.remove('text-gray-500');
                            icon.classList.add('text-yellow-400');
                        } else {
                            icon.classList.remove('text-yellow-400');
                            icon.classList.add('text-gray-500');
                        }
                        
                        updateFavorites();
                    }
                }
            });
            
            // Keyboard navigation
            document.addEventListener('keydown', (e) => {
                if (e.key === 'ArrowLeft' && currentChannelIndex > 0) {
                    currentChannelIndex--;
                    playChannel(channels[currentChannelIndex], currentChannelIndex);
                } else if (e.key === 'ArrowRight' && currentChannelIndex < channels.length - 1) {
                    currentChannelIndex++;
                    playChannel(channels[currentChannelIndex], currentChannelIndex);
                }
            });
            
            // Initialize
            loadChannels();
            updateFavorites();
            
            // Play first channel by default
            if (channels.length > 0) {
                playChannel(channels[0], 0);
            }
        });
    </script>
</body>
</html>
