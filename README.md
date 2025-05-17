-- LocalScript para aumentar FPS ao máximo (removendo texturas e efeitos pesados)
local lighting = game:GetService("Lighting")
local terrain = workspace:FindFirstChildOfClass("Terrain")

-- Remove texturas e decals
for _, obj in ipairs(workspace:GetDescendants()) do
	if obj:IsA("Texture") or obj:IsA("Decal") or obj:IsA("SurfaceAppearance") then
		obj:Destroy()
	elseif obj:IsA("MeshPart") then
		obj.TextureID = ""
	elseif obj:IsA("Part") or obj:IsA("UnionOperation") or obj:IsA("MeshPart") then
		obj.Material = Enum.Material.SmoothPlastic
	end
end

-- Remove efeitos de iluminação
lighting.GlobalShadows = false
lighting.FogEnd = 1000000
lighting.Brightness = 0
lighting.EnvironmentDiffuseScale = 0
lighting.EnvironmentSpecularScale = 0

-- Remove partículas e efeitos
for _, v in ipairs(workspace:GetDescendants()) do
	if v:IsA("ParticleEmitter") or v:IsA("Trail") or v:IsA("Smoke") or v:IsA("Fire") then
		v:Destroy()
	end
end

-- Desativa água e sombras do terreno
if terrain then
	terrain.WaterTransparency = 1
	terrain.WaterWaveSize = 0
	terrain.WaterReflectance = 0
end

-- (Opcional) Remove objetos desnecessários de cenário
for _, obj in ipairs(workspace:GetDescendants()) do
	if obj:IsA("Model") and not obj:FindFirstChildOfClass("Humanoid") then
		-- obj:Destroy() -- ⚠️ CUIDADO: isso apaga modelos. Ative se tiver certeza!
	end
end

print("Boost de FPS ativado. Texturas removidas.")
